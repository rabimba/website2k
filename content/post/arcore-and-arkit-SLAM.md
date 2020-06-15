---
title: 'ARCore and Arkit, What is under the hood: SLAM (Part 2)'
date: 2018-10-30T04:30:00.001-05:00
draft: false
aliases: [ "/2018/10/arcore-and-arkit-SLAM.html" ]
tags : [webxr, arcore, arkit, mozilla]
---

[![](https://1.bp.blogspot.com/-uu4M7kal1Ao/W9c1B5zC11I/AAAAAAAB93Q/8TVyWxzYcXATX1xgZoqR4UepYqdMTExugCLcBGAs/s320/arcore-arkit.jpg)](https://1.bp.blogspot.com/-uu4M7kal1Ao/W9c1B5zC11I/AAAAAAAB93Q/8TVyWxzYcXATX1xgZoqR4UepYqdMTExugCLcBGAs/s1600/arcore-arkit.jpg)

In our last blog post ([part 1](https://blog.rabimba.com/2018/10/arcore-and-arkit-what-is-under-hood.html)), we took a look at how algorithms detect keypoints in camera images. These form the basis of our world tracking and environment recognition. But for Mixed Reality, that alone is not enough. We have to be able to calculate the 3d position in the real world. It is often calculated by the spatial distance between itself and multiple keypoints. This is often called Simultaneous Localization and Mapping (SLAM). And this is what is responsible for all the world tracking we see in ARCore/ARKit.

  

### What we will cover today:

*   How ARCore and ARKit does it's SLAM/Visual Inertia Odometry
*   Can we D.I.Y our own SLAM with reasonable accuracy to understand the process better

Sensing the world: as a computer
--------------------------------

[![](https://2.bp.blogspot.com/-vC298Yf2zGk/W9fyprdS2tI/AAAAAAAB930/r7cVY8bGSsA_rgo070UUMq8Zn2cyh_WywCK4BGAYYCw/s320/photo_2018-10-30_00-55-46.jpg)](http://2.bp.blogspot.com/-vC298Yf2zGk/W9fyprdS2tI/AAAAAAAB930/r7cVY8bGSsA_rgo070UUMq8Zn2cyh_WywCK4BGAYYCw/s1600/photo_2018-10-30_00-55-46.jpg)When we start any augmented reality application in mobile or elsewhere, the first thing it tries to do is to detect a plane. When you first start any MR app in ARKit, ARCore, the system doesn't know anything about the surroundings. It starts processing data from camera and pairs it up with other sensors.

Once it has those data it tries to do the following two things

1.  **Build a point cloud mesh** of the environment by building a map
2.  **Assign a relative position of the device** within that perceived environment

From our [previous article](https://blog.rabimba.com/2018/10/arcore-and-arkit-what-is-under-hood.html), we know it's not always easy to build this map from unique feature points and maintain that. However, that becomes easy in certain scenarios if you have the freedom to place _beacons_ at different known locations. Something [we did at Mozfest 2016](https://blog.rabimba.com/2017/03/mozilla-festival-recap.html) when Mozilla still had the Magnets project which we had utilized as our beacons. A similar approach is used in a few museums for providing turn by turn navigation to point of interests as their indoor navigation system. However Augmented Reality systems don't have this luxury.

A little saga about relationships
---------------------------------

We will start with a map.....about relationships. Or rather "[A Stochastic Map For Uncertain Spatial Relationships](https://pdfs.semanticscholar.org/76a6/c5352a0fbc3fec5395f1501b58bd6566d214.pdf)" by Smith et al. 

In the real world, you have precise and correct information about the exact location of every object. However in AR world that is not the case. For understanding the case lets assume we are in an empty room and our mobile has detected a **reliable unique anchor (A)** (or that can be a stationary beacon) and our position is at **(B). **  

[![](https://3.bp.blogspot.com/-sn28jxDs5Fw/W9gLoh5H6JI/AAAAAAAB94M/IV0auj81GowfLpJwM9tD7F0iF5gZO80JQCLcBGAs/s1600/Capture.PNG)](https://3.bp.blogspot.com/-sn28jxDs5Fw/W9gLoh5H6JI/AAAAAAAB94M/IV0auj81GowfLpJwM9tD7F0iF5gZO80JQCLcBGAs/s1600/Capture.PNG)

In a perfect situation, we know the distance between A and B, and if we want to move towards **C** we can infer exactly how we need to move.  

[![](https://2.bp.blogspot.com/-bAuhtRT538U/W9gL77GM00I/AAAAAAAB94Y/pPfVVDLAksYEFf_-5K1TZT9lFyGYWRAkQCLcBGAs/s1600/Capture.PNG)](https://2.bp.blogspot.com/-bAuhtRT538U/W9gL77GM00I/AAAAAAAB94Y/pPfVVDLAksYEFf_-5K1TZT9lFyGYWRAkQCLcBGAs/s1600/Capture.PNG)

  

Unfortunately, in the world of AR and SLAM we need to work with imprecise knowledge about the position of A and C. This results in uncertainties and the need to continually correct the locations. 

[![](https://3.bp.blogspot.com/-UcX24P1vCOs/W9gM7N9mWWI/AAAAAAAB94g/0xHOo_0r-KwhbOrUrVEG9O0qzJmEVNhRgCLcBGAs/s1600/Capture.PNG)](https://3.bp.blogspot.com/-UcX24P1vCOs/W9gM7N9mWWI/AAAAAAAB94g/0xHOo_0r-KwhbOrUrVEG9O0qzJmEVNhRgCLcBGAs/s1600/Capture.PNG)

  

The points have a relative spatial relationship with each other and that allows us to get a probability distribution of every possible position. Some of the common methods to deal with the uncertainty and correct positioning errors are **Kalman ****Filter** (this is what we used in Mozfest), _Maximum Posteriori Estimation_ or _Bundle Adjustment. _

Since these estimations are not perfect, every new sensor update also has to update the estimation model.

### Aligning the Virtual World

To map our surroundings reliably in Augmented Reality, we need to continually update our measurement data. The assumptions are, every sensory input we get contains some inaccuracies. We can take help from Milios et al in their paper "[Globally Consistent Range Scan Alignment for Environment Mapping](https://link.springer.com/article/10.1023/A:1008854305733)" to understand the issue. 

[![](https://4.bp.blogspot.com/-U_DAfEvu9J0/W9gSUw60h0I/AAAAAAAB94w/TPltedn8cQ0hNW4Cslgska4QJ8aB8Er4gCLcBGAs/s1600/Capture.PNG)](https://4.bp.blogspot.com/-U_DAfEvu9J0/W9gSUw60h0I/AAAAAAAB94w/TPltedn8cQ0hNW4Cslgska4QJ8aB8Er4gCLcBGAs/s1600/Capture.PNG)

_Image credits: Lu, F., & Milios, E. (1997). Globally consistent range scan alignment for environment mapping_

Here in figure a, we see how going from position P1....Pn accumulates little measurement errors over time until the resulting environment map is wrong. But when we align the scan sin fig b, the result is considerably improved. To do that, the algorithm keeps track of all local frame data and network spatial relations among those.

A common problem at this point is how much data to store to keep doing the above correctly. Often to reduce complexity level the algorithm reduces the keyframes it stores.

  

Let's build the map a.k.a SLAM
------------------------------

To make Mixed Reality feasible, SLAM has the following challenges to handle

1.  Monocular Camera input
2.  Real-time
3.  Drift

### Skeleton of SLAM

How do we deal with these in a Mixed Reality scene?

We start with the principles by Cadena et. al in their "[Past, Present, and Future of Simultaneous Localization and Mapping: Toward the Robust-Perception Age](https://ieeexplore.ieee.org/abstract/document/7747236/)" paper. From that paper, we can see the standard architecture of SLAM to be something like

[![](https://4.bp.blogspot.com/-pnk1QWmyLq8/W9gWtDP3qhI/AAAAAAAB948/s5QvcvOTGSUg-LAogTggBfNUFZqntvfRACLcBGAs/s1600/Capture.PNG)](https://4.bp.blogspot.com/-pnk1QWmyLq8/W9gWtDP3qhI/AAAAAAAB948/s5QvcvOTGSUg-LAogTggBfNUFZqntvfRACLcBGAs/s1600/Capture.PNG)

Image Credit: Cadena et al

If we deconstruct the diagram we get the following four modules

1.  **Sensor**: On mobiles, this is primarily Camera, augmented by accelerometer, gyroscope and depending on the device light sensor. Apart from Project Tango enabled phones, nobody ahd depth sensor for Android.
2.  **Front End:** The feature extraction and anchor identification happens here [as we described in previous post](https://blog.rabimba.com/2018/10/arcore-and-arkit-what-is-under-hood.html).
3.  **Back End**: Does error correction to compensate for the drift and also takes care of localizing pose model and overall geometric reconstruction.
4.  **SLAM estimate**: This is the result containing the tracked features and locations.

To better understand it, we can take a look at one of the open source implementations of SLAM.

  

### D.I.Y SlAM: Taking a peek at ORB-SLAM

To try our hands on to understand how SLAM works let's take a look at a recent algorithm by Montiel et al called [ORB-SLAM](http://webdiis.unizar.es/~raulmur/orbslam/). We will use the code of its successor [ORB-SLAM2](https://github.com/raulmur/ORB_SLAM2). The algorithm is available in Github under GPL3 and I found this excellent blog which goes into nifty details on [how we can run ORB-SLAM2 in our computer](https://medium.com/@j.zijlmans/orb-slam-2052515bd84c). I highly encourage you to read that to avoid encountering problems at the setup.

His talk is also available here to see and is very interesting

  

  
ORB-SLAM just uses the camera and doesn't utilize any other gyroscope or accelerometer inputs. But the result is still impressive.  

#### 

1.  Detecting Features: ORB-SLAM, as the name suggests uses [ORB](https://ieeexplore.ieee.org/abstract/document/6126544/) to find keypoint and generate binary descriptors. Internally ORB is based on the same method to find keypoint and generating binary descriptors [as we discussed in part 1 for BRISK](https://blog.rabimba.com/2018/10/arcore-and-arkit-what-is-under-hood.html). In short ORB-SLAM analyzes each picture to find keyframe and then store it with a reference to the keyframe in a map. These are utilized in future to correct historical data.
2.  Keypoint > 3d landmark: The algorithm looks for new frames from the image and when it finds one it performs keypoint detection on it. These are then matched with the previous frame to get a spatial distance. This so far provides a good idea on where it can find the same key points again in a new frame. This provides the initial camera pose estimation.
3.  Refine Camera Pose: The algorithm repeats Step 2 by projecting the estimated initial camera pose into next camera frame to search for more keypoint which corresponds to the one it already knows. If it is certain it can find them, it uses the additional data to refine the pose and correct any spatial measurement error.

[![](https://2.bp.blogspot.com/-d40aOrImMNw/W9geNFRnnqI/AAAAAAAB95I/uEokK7Q_WlQw6tucCs4D4DuQoC6GCn8RgCLcBGAs/s1600/Capture.PNG)](https://2.bp.blogspot.com/-d40aOrImMNw/W9geNFRnnqI/AAAAAAAB95I/uEokK7Q_WlQw6tucCs4D4DuQoC6GCn8RgCLcBGAs/s1600/Capture.PNG)

green squares  = tracked keypoints. Blue boxes: keyframes. Red box = camera view. Red points = local map points.  
_Image credits: ORB-SLAM video by Raúl Mur Artal_

###   
Returning home a.k.a Loop Closing

One of the goals of MR is when you walk back to your starting point it should understand you have returned. The inherent inefficiency and the induced error make it hard to accurately predict this. This is called loop closing for SLAM. ORB-SLAM handles it by defining a threshold. It tries to match keypoints in a frame with next frames and if the previously detected frames matching percentage exceeds a threshold then it knows you have returned.

[![](https://4.bp.blogspot.com/-bxhoz71ks2U/W9gf1lXwNuI/AAAAAAAB95U/f5jsjgHszkIO4M5-PjDCuswZ34si_MoPACLcBGAs/s1600/Capture.PNG)](https://4.bp.blogspot.com/-bxhoz71ks2U/W9gf1lXwNuI/AAAAAAAB95U/f5jsjgHszkIO4M5-PjDCuswZ34si_MoPACLcBGAs/s1600/Capture.PNG)

Loop Closing performed by the ORB-SLAM algorithm.  
_Image credits: Mur-Artal, R., Montiel_

To account for the error, the algorithm has to propagate coordinate correction throughout the whole frame with updated knowledge to know the loop should be closed

[![](https://2.bp.blogspot.com/-5E5V32biAoY/W9ggaLdAI6I/AAAAAAAB95c/WEl0yQG-OjwlP6mdmVO9ovMLlHv_BgknwCLcBGAs/s1600/Capture.PNG)](https://2.bp.blogspot.com/-5E5V32biAoY/W9ggaLdAI6I/AAAAAAAB95c/WEl0yQG-OjwlP6mdmVO9ovMLlHv_BgknwCLcBGAs/s1600/Capture.PNG)

The reconstructed map before (up) and after (down) loop closure.  
_Image credits: Mur-Artal, R., Montiel_

SLAM today:
-----------

### Google: [ARCore's documentation](https://developers.google.com/ar/discover/concepts) describes it's tracking method as "concurrent odometry and mapping" which is essentially SLAM+sensor inputs. Their [patent](https://patents.google.com/patent/US20170336511A1/en) also indicates they have included inertial sensors into the design.

### Apple: Apple also is using [Visual Interial Odometry](https://medium.com/6d-ai/why-is-arkit-better-than-the-alternatives-af8871889d6a) which they acquired by buying Metaio and FlyBy. I learned a lot about what they are doing by having a look at this [video](https://developer.apple.com/videos/play/wwdc2018/610/) at WWDC18.

Additional Read: I found this "[A comparative analysis of tightly-coupled monocular, binocular, and stereo VINS](https://ieeexplore.ieee.org/document/7989022/)" paper to be a nice read to see how different IMU's are used and compared. IMU's are the devices that provide all this sensory data to our devices today. And their calibration is supposed to be crazy difficult. 

  

I hope this post along with the [previous one](https://blog.rabimba.com/2018/10/arcore-and-arkit-what-is-under-hood.html) provides a better understanding of how our world is tracked inside ARCore/ARKit.

  

In a few days, I will start another blog series on how to build Mixed Reality applications and use experimental as well as some stable WebXR api's to build Mixed Reality application demos.

As always feedbacks are welcome.

  

#### References/Interesting Reads:

*   [A stochastic map for uncertain spatial relationships](https://pdfs.semanticscholar.org/76a6/c5352a0fbc3fec5395f1501b58bd6566d214.pdf)
*   [Globally consistent range scan alignment for environment mapping](https://link.springer.com/article/10.1023/A:1008854305733)
*   [ORB-SLAM](https://ieeexplore.ieee.org/iel7/8860/4359257/07219438.pdf)
*   [Past, Present, and Future of Simultaneous Localization and Mapping: Towards the Robust-Perception Age](https://ieeexplore.ieee.org/abstract/document/7747236/)
*   [ORB feature tracking algorithm](https://ieeexplore.ieee.org/abstract/document/6126544/)
*   [A Comparative Analysis of Tightly-coupled Monocular, Binocular, and Stereo VINS](https://ieeexplore.ieee.org/document/7989022/)
*   [Semantic Visual Localization](http://openaccess.thecvf.com/content_cvpr_2018/CameraReady/0849.pdf) (this might just be future)

The first part of this lives here: [https://blog.rabimba.com/2018/10/arcore-and-arkit-what-is-under-hood.html ](https://blog.rabimba.com/2018/10/arcore-and-arkit-what-is-under-hood.html)