---
title: "3D Image Reconstruction Basics"
date: 2018-01-28
tags: [COnstructing a 3D image from multiple 2D images, 3D reconstruction, Image Reconstruction]
header:
  image: "/images/personal/reconstruction.jpeg"
excerpt: "3D Image Reconstruction"
mathjax: "true"
---

In Computer Vision, the classification of scenes, objects and activities, along with the output of bounding boxes and image segmentation is, as we have seen, the focus of much new research. In essence, these approaches apply computation to gain an ‘understanding’ of the 2D space of an image. However, detractors note that a 3D understanding is imperative for systems to successfully interpret, and navigate, the real world.
For instance, a network may locate a cat in an image, colour all of its pixels and classify it as a cat. But does the network fully understand where the cat in the image is, in the context of the cat’s environment?
One could argue that the computer learns very little about the 3D world from the above tasks. Contrary to this, humans understand the world in 3D even when examining 2D pictures, i.e. perspective, occlusion, depth, how objects in a scene are related, etc. Imparting these 3D representations and their associated knowledge to artificial systems represents one of the next great frontiers of Computer Vision.

However, 3D understanding has traditionally faced several impediments. The first concerns the problem of both ‘self and normal occlusion’ along with the numerous 3D shapes which fit a given 2D representation. Understanding problems are further compounded by the inability to map different images of the same structures to the same 3D space, and in the handling of the multi-modality of these representations [94]. Finally, ground-truth 3D datasets were traditionally quite expensive and difficult to obtain which, when coupled with divergent approaches for representing 3D structures, may have led to training limitations.

#Reconstruction Methods

The field itself comprises many different types of reconstruction, e.g. scene reconstruction, multi-view and single view reconstruction, structure from motion (SfM), SLAM, etc. Furthermore, some reconstruction approaches leverage additional (and multiple) sensors and equipment, such as Event or RGB-D cameras, and can often layer multiple techniques to drive progress.
The result? Whole scenes can be reconstructed non-rigidly and change spatio-temporally, e.g. a high-fidelity reconstruction of yourself, and your movements, updated in real-time.
As identified previously, issues persist around the mapping of 2D images to 3D space. The following papers present a plethora of approaches to create high-fidelity, real-time reconstructions:

#Fusion4D: Real-time Performance Capture of Challenging Scenes 
It veers towards the domain of Computer Graphics, however the interplay between Computer Vision and Graphics cannot be overstated. The authors’ approach uses RGB-D and Segmentation as inputs to form a real-time, multi-view reconstruction which is outputted using Voxels.
Fusion4D creates real-time, high fidelity voxel representations which have impressive applications in virtual reality, augmented reality and telepresence. This work from Microsoft will likely revolutionise motion capture, possibly for live sports.

#Real-Time 3D Reconstruction and 6-DoF Tracking with an Event Camera 
This technique won best paper at the European Convention on Computer Vision (ECCV) in 2016. The authors propose a novel algorithm capable of tracking 6D motion and various reconstructions in real-time using a single Event Camera.
The Event camera is gaining favour with researchers in Computer Vision due to its reduced latency, lower power consumption and higher dynamic range when compared to traditional cameras. Instead of a sequence of frames outputted by a regular camera, the event camera outputs “a stream of asynchronous spikes, each with pixel location, sign and precise timing, indicating when individual pixels record a threshold log intensity change.” 

#Unsupervised CNN for Single View Depth Estimation: Geometry to the Rescue
 It proposes an unsupervised method for training a deep CNN for single view depth prediction with results comparable to SOTA using supervised methods. Traditional deep CNN approaches for single view depth prediction require large amounts of manually labelled data, however unsupervised methods again demonstrate their value by removing this necessity. The authors achieve this “by training the network in a manner analogous to an autoencoder”, using a stereo-rig.