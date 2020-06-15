---
title: 'ARCore and Arkit: What is under the hood : Anchors and World Mapping (Part 1)'
date: 2018-10-29T02:54:00.000-05:00
draft: false
aliases: [ "/2018/10/arcore-and-arkit-what-is-under-hood.html" ]
tags : [webxr, arcore, mozilla]
---

[![](https://1.bp.blogspot.com/-WZXM9DE3gEQ/W9XmOH_td_I/AAAAAAAB9zg/bK1NaxuHswgjTCl1ImJrq38b26ZVuscFACLcBGAs/s320/arcore-arkit.jpg)](https://1.bp.blogspot.com/-WZXM9DE3gEQ/W9XmOH_td_I/AAAAAAAB9zg/bK1NaxuHswgjTCl1ImJrq38b26ZVuscFACLcBGAs/s1600/arcore-arkit.jpg)

_Reading Time: 7 MIn_  
Some of you know I have been recently experimenting a bit more with WebXR than a WebVR and when we talk about mobile Mixed Reality, ARkit and ARCore is something which plays a pivotal role to map and understand the environment inside our applications.

  

I am planning to write a series of blog posts on how you can start developing WebXR applications now and play with them starting with the basics and then going on to using different features of it. But before that, I planned to pen down this series of how actually the "world mapping" works in arcore and arkit. So that we have a better understanding of the Mixed Reality capabilities of the devices we will be working with.

  

Mapping: feature detection and anchors
--------------------------------------

Creating apps that work seamlessly with arcore/kit requires a little bit of knowledge about the algorithms that work in the back and that involves knowing about Anchors.

### What are anchors:

Anchors are your virtual markers in the real world. As a developer, you anchor any virtual object to the real world and that 3d model will stay glued into the physical location of the real world. Anchors also get updated over time depending on the new information that the system learns. For example, if you anchor a pikcahu 2 ft away from you and then you actually walk towards your pikachu, it realises the actual distance is 2.1ft, then it will compensate that. In real life we have a static coordinate system where every object has it's own x,y,z coordinates. Anchors in devices like HoloLens [override the rotation and position](https://docs.unity3d.com/Manual/wmr_input_types.html) of the transform component.

### How Anchors stick?

If we follow the d[ocumentation in Google ARCore](https://developers.google.com/ar/develop/developer-guides/anchors#use_anchors_in_your_scene) then we see it is attached to something called "trackables", which are feature points and planes in an image. Planes are essentially clustered feature points. You can have a more in-depth look at what Google says ARCore anchor does by reading their really nice [Fundamentals](https://developers.google.com/ar/discover/concepts). But for our purposes, we first need to understand what exactly are these Feature Points.

### Feature Points: through the eyes of computer vision

Feature points are distinctive markers on an image that an algorithm can use to track specific things in that image. Normally any distinctive pattern, such as T-junctions, corners are a good candidate. They lone are not too useful to distinguish between each other and reliable place marker on an image so the neighbouring pixels of that image are also analyzed and saved as a descriptor.

Now a good anchor should have reliable feature points attached to it. The algorithm must be able to find the same physical space under different viewpoints. It should be able to accommodate the change in 

*   Camera Perspective
*   Rotation
*   Scale
*   Lightning
*   Motion blur and noise

#### Reliable Feature Points

This is an open research problem with multiple solutions on board. Each with their own set of problems though. One of the most popular algorithms stem from this [paper](https://link.springer.com/article/10.1023/B:VISI.0000029664.99615.94) by David G. Lowe at IJCV is called Scale Invariant Feature Transform ([SIFT](https://link.springer.com/article/10.1023/B:VISI.0000029664.99615.94)). Another follow up work which claims to have even better speed was published in ECCV in 2006 called Speeded Up Robust Features ([SURF](https://link.springer.com/article/10.1023/B:VISI.0000029664.99615.94)) by Bay et al. Thought both of them are [patented](https://patents.google.com/patent/US6711293) at this point. 

  

Microsoft Hololens doesn't really need to do all this heavy lifting since it can rely on an extensive amount of sensor data. Especially it gets aid from the depth sensor data from its [Infrared Sensors](https://blog.kloud.com.au/2017/12/15/hololens-understanding-depth-spatial-mapping/). However, ARCore and ARkit doesn't enjoy those privileges and has to work with 2d images. Though we cannot say for sure which of the algorithm is actually used for ARKit or ARCore we can try to replicate the procecss with a patent-free algorithm to understand how the process actually works.

  

D.I.Y Feature Detection and keypoint descriptors
------------------------------------------------

To understand the process we will use an algorithm by Leutenegger et al called [BRISK](https://www.research-collection.ethz.ch/bitstream/handle/20.500.11850/43288/eth-7684-01.pdf?sequence=1). To detect feature we must follow a multi-step process. A typical algorithm would adhere to the following two steps

1.  **_Keypoint Detection_**: Detecting keypoint can be as simple as just detecting corners. Which essentially evaluates the contrast between neighbouring pixels. A common way to do that in a large-scale image is to blur the image to smooth out pixel contrast variation and then do edge detection on it. The rationale for this is that you would normally want to detect a tree and a house as a whole to achieve reliable tracking instead of every single twig or window. SIFT and SURF adhere to this approach. However, for real-time scenario blurring adds a compute penalty which we don't want. In their paper "[Machine Learning for High-Speed Corner Detection](https://link.springer.com/chapter/10.1007%2F11744023_34)" Rosten and Drummond proposed a method called FAST which analyzes the circular surrounding if each pixel _p._ If the neighbouring pixels brightness is lower/higher than _p _ and a certain number of connected pixels fall into this category then the algorithm found a corner. 
    
    [![](https://4.bp.blogspot.com/-kmtsWv-iLV8/W9asnmE1SvI/AAAAAAAB91w/93DoNXkJpUI17o_CrwCJeHEg8DBdJ9pgwCLcBGAs/s1600/Capture.PNG)](https://4.bp.blogspot.com/-kmtsWv-iLV8/W9asnmE1SvI/AAAAAAAB91w/93DoNXkJpUI17o_CrwCJeHEg8DBdJ9pgwCLcBGAs/s1600/Capture.PNG)
    
    _Image credits: Rosten E., Drummond T. (2006) Machine Learning for High-Speed Corner Detection.. Computer Vision – ECCV 2006. _
    
    Now back to BRISK, for it out of the 16-pixel circle, 9 consecutive pixels must be brighter or darker than the central one. Also BRISk uses down-sized images allowing it to achieve better invariance to scale.
2.  _Keypoint Descriptor:_ The primary property of the detected keypoints should be that they are unique. The algorithm should be able to find the feature in a different image with a different viewpoint, lightning. BRISK concatenates the brightness comparison results between different pixels surrounding the centre keypoint and concatenates them to a 512 bit string.
    
    [![](https://1.bp.blogspot.com/-V8mHJzUMG18/W9av0X0y1jI/AAAAAAAB918/xtN4YD_kFww62DUL23tbH0q2b-jezWlsACLcBGAs/s1600/Capture.PNG)](https://1.bp.blogspot.com/-V8mHJzUMG18/W9av0X0y1jI/AAAAAAAB918/xtN4YD_kFww62DUL23tbH0q2b-jezWlsACLcBGAs/s1600/Capture.PNG)
    
    _Image credits: S. Leutenegger, M. Chli and R. Y. Siegwart, “BRISK: Binary Robust invariant scalable keypoints”, 2011 International Conference on Computer Vision_
    
    As we can see from the sample figure, the blue dots create the concentric circles and the red circles indicate the individually sampled areas. Based on these, the results of the brightness comparison are determined. BRISK also ensures rotational invariance. This is calculated by the largest gradients between two samples with a long distance from each other.

### Test out the code

To test out the algorithms we will use the reference implementations available in OpenCV. We can use a pip install to install it with python bindings

  

As test image, I used two test images I had previously captured in my talks at All Things Open and TechSpeaker meetup. One is an evening shot of Louvre, which should have enough corners as well as overlapping edges, and another a picture of my friend in a beer garden in portrait mode. To see how it fares against the already existing blur on the image.  
  

[![](https://4.bp.blogspot.com/-bD75lqYYPas/W9a2BWrBi7I/AAAAAAAB92I/ZuhU_4Twu0MPfdU7H0vcervl-LhFtQ3bACLcBGAs/s400/dgp.jpg)](https://4.bp.blogspot.com/-bD75lqYYPas/W9a2BWrBi7I/AAAAAAAB92I/ZuhU_4Twu0MPfdU7H0vcervl-LhFtQ3bACLcBGAs/s1600/dgp.jpg)

[Original Image Link](https://photos.app.goo.gl/3AHhTjkHcXBsoJSf7)

  

[![](https://2.bp.blogspot.com/-5h1gKSKafg4/W9a2Bs08nXI/AAAAAAAB92M/Z-d-jH2TB-Ie3GQRPaGb7ulS4E1AsQtJACLcBGAs/s400/paris.jpg)](https://2.bp.blogspot.com/-5h1gKSKafg4/W9a2Bs08nXI/AAAAAAAB92M/Z-d-jH2TB-Ie3GQRPaGb7ulS4E1AsQtJACLcBGAs/s1600/paris.jpg)

[Original Image Link](https://photos.app.goo.gl/MXgsD36sLT47tER26)

#### Visualizing the Feature Points

We use the below small code snippet to use BRISK on the two images above to visualize the feature points

  

  
What the code does:  

1.  Loads the jpeg into the variable and converts into grayscale
2.  Initialize BRISK and run it. We use the paper suggested 4 octaves and an increased threshold of 70. This ensures we get a low number but highly reliable key points. As we will see below we still got a lot of key points
3.  We used the detectAndCompute() to get two arrays from the algo holding both the keypoints and their descriptors
4.  We draw the keypoints at their detected positions indicating keypoint size and orientation through circle diameter and angle, The "DRAW\_MATCHES\_FLAGS\_DRAW\_RICH\_KEYPOINTS" does that.

[![](https://3.bp.blogspot.com/-kUNd9WX39NY/W9a5PXwT_8I/AAAAAAAB928/xKGRexbB_RE2QIqB2saQHJX6jeTt6p48wCLcBGAs/s1600/brisk_keypoints.jpg)](https://3.bp.blogspot.com/-kUNd9WX39NY/W9a5PXwT_8I/AAAAAAAB928/xKGRexbB_RE2QIqB2saQHJX6jeTt6p48wCLcBGAs/s1600/brisk_keypoints.jpg)

  

[![](https://3.bp.blogspot.com/-a_DFYvX0Lps/W9a5PUphjwI/AAAAAAAB924/6cC8NqKv4ykYqryBkes5EE9az79CWE4YACLcBGAs/s1600/brisk_keypoints_dgp.jpg)](https://3.bp.blogspot.com/-a_DFYvX0Lps/W9a5PUphjwI/AAAAAAAB924/6cC8NqKv4ykYqryBkes5EE9az79CWE4YACLcBGAs/s1600/brisk_keypoints_dgp.jpg)

  

As you can see most of the key points are visible at the castle edges and all visible edges for Louvre and almost none on the floor. With the portrait mode pic of my friend it's more diverse but also shows some false positives like the reflection on the glass. Considering how BRISK works, this is normal.

  

Conclusion
----------

In this first part of understanding what power ARCore/Kit we understood how basic feature detection works behind the scenes and tried our hands on to replicate that. These spatial anchors are vital to the virtual objects "glueing" to the real world. This whole demo and hands-on now should help you understand why designing your apps **so that users place objects in areas where the device has a chance to create anchors** is a good idea.

Placing a lot of objects in a single non-textured smooth plane may produce inconsistent experience since its just too hard to detect keypoints in a plane surface (**now you know why**). As a result, the objects may sometimes drift away if tracking is not good enough.

If your app design encourages placing objects near corners of floor or table then the app has a much better chance of working reliably. Also, Google's guide on anchor placement is an excellent read.

  

Their short recommendation is:

*   **Release spatial anchors if you don’t need them.** Each anchor costs CPU cycles which you can save
*   **Keep the object close to the anchor.** 

On our [next post](https://blog.rabimba.com/2018/10/arcore-and-arkit-SLAM.html), we will see how we can use this knowledge to do basic SLAM.  
  
**Update:** The next post lives here: [https://blog.rabimba.com/2018/10/arcore-and-arkit-SLAM.html](https://blog.rabimba.com/2018/10/arcore-and-arkit-SLAM.html)