---
title: 'Hosting 360 Degree Videos and Images in a CORS Supported Server'
date: 2016-03-22T23:41:00.000-05:00
draft: false
aliases: [ "/2016/03/hosting-360-degree-videos-and-images-in.html" ]
---

**Why**: If you have been playing with 360 degree videos and images like me in the recent past (specially with the awesome release of [Mozilla aframe.io](https://aframe.io/)) then probably you are looking for an inexpensive or preferable free place to host your images/videos since most of the free places where we can upload them don't support CORS.  
  
**How: **  

#### Using AWS to Host 360° Virtual Reality Panoramas & 360° Video

  

[AWS S3](http://aws.amazon.com/s3/) has no inode limit and works especially well with multi-res panorama. AWS S3 also works well for large streaming 360° Video Files.

  

#### Create an AWS S3 Account

If you do not already have an AWS S3 account, sign up for a [Free Amazon Web Services Trial Account](http://aws.amazon.com/free/), see the following video for details

* * *

#### Create a Bucket

Once you have created your account you will need to create at least one Bucket, see the following video for simple instructions if you are not already familiar with basics of using AWS S3

* * *

#### Set permissions for your bucket

use the AWS web interface to set [AWS Bucket Policy](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-iam-policies.html) & [CORS Configuration](http://docs.aws.amazon.com/AmazonS3/latest/dev/cors.html), setting these as below will automatically set public read access permissions for all files in that bucket, otherwise you will have to set permission per file and may have trouble viewing your panoramas

  

* * *

#### AWS S3 Bucket Permissions: Bucket Policy and CORS Configuration

Go to your "All Buckets" list on your S3 page, click on the "Properties" button in the upper right, select your bucket, and click on the "Permissions" option, and set the following -

#### Edit Bucket Policy -

_Replace MY\_BUCKET\_NAME with the name of the bucket you are editing_

> {
> 
> "Version":  "2008-10-17",
> 
> "Id":  "http referer policy example",
> 
> "Statement":  \[
> 
> {
> 
> "Sid":  "readonly policy",
> 
> "Effect":  "Allow",
> 
> "Principal":  "\*",
> 
> "Action":  "s3:GetObject",
> 
> "Resource":  "arn:aws:s3:::MY\_BUCKET\_NAME/\*"
> 
> }
> 
> \]
> 
> }

#### Add CORS Configuration

> <CORSRule\>
> 
> <AllowedOrigin\>http://\*

<AllowedOrigin\>https://\*

<AllowedMethod\>GET</AllowedMethod\>

<MaxAgeSeconds\>3000</MaxAgeSeconds\>

<AllowedHeader\>Authorization</AllowedHeader\>

</CORSRule\>

</CORSConfiguration\>

#### Uploading Panoramas

You can upload your panoramas to AWS S3 either using the[web interface](http://docs.aws.amazon.com/AmazonS3/latest/UG/UploadingObjectsintoAmazonS3.html), or with ftp clients such as[Cyberduck](https://cyberduck.io/)or [Transmit](http://panic.com/transmit/), and[many others](http://www.labnol.org/internet/amazon-s3-clients-roundup/8286/)