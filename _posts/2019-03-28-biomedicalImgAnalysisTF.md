---
title: "Biomedical Image Analysis using Tensorflow"
date: 2019-03-28
tags: [Farmako, Healthcare, Medical Imaging]
header:
  image: "/images/personal/examplesOfMedicalImages.png"
excerpt: "Farmako, Deep Learning"
mathjax: "true"
---

# What is biomedical image analysis and why is it needed? 
Biomedical images are measurements of the human body on different scales (i.e. microscopic, macroscopic, etc.). They come in a wide variety of imaging modalities (e.g. a CT scanner, an ultrasound machine, etc.) and measure a physical property of the human body (e.g. radiodensity, the opacity to X-rays). These images are interpreted by domain experts (e.g. a radiologist) for clinical tasks (e.g. a diagnosis) and have a large impact on decision making of physicians.

Biomedical images are typically volumetric images (3D) and sometimes have an additional time dimension (4D) and/or multiple channels (4-5D) (e.g. multi-sequence MR images). The variation in biomedical images is quite different from that of a natural image (e.g. a photograph), as clinical protocols aim to stratify how an image is acquired (e.g. a patient is lying on his/her back, the head is not tilted, etc.). In their analysis, we aim to detect subtle differences (i.e. some small region indicating an abnormal finding).

#H3 Why computer vision and machine learning? 
Computer vision methods have long been employed to automatically analyze biomedical images. The recent advent of deep learning has replaced many other machine learning methods, because it avoids the creation of hand-engineering features, thus removing a critical source of error from the process. Additionally, the fast inference speeds of GPU-accelerated fully networks, allows us scale analyses to unprecedented amounts of data (e.g. 10⁶ subject images).

# Can we readily employ deep learning libraries for biomedical imaging?
While many deep learning libraries expose low-level operations (e.g. tensor multiplications, etc.) to the developers, a lot of the higher-level specialty operations are missing for their use on volumetric images (e.g. differentiable 3D upsampling layers, etc.), and due to the additional spatial dimension(s) of the images, we can run into memory issues (e.g. storing a single copy of a database of 1k CT images, with image dimensions of 512x512x256 voxels in float32 is ~268 GB). Due to the different nature of acquisition, some images will require special pre-processing (e.g. intensity normalization, bias-field correction, de-noising, spatial normalization/registration, etc).

# Some example applications for instance
With all the basic knowledge provided in blogs given by DLTK, we can now look into building full applications for deep learning on medical images with TensorFlow. 

# Image segmentation of multi-channel brain MR images
This image segmentation application learns to predict brain tissues and white matter lesions from multi-sequence MR images (T1-weighted, T1 inversion recovery and T2 FLAIR) on the small (N=5) MRBrainS challenge dataset. It uses a 3D U-Net-like network with residual units as feature extractors and tracks the Dice coefficient accuracy for each label in TensorBoard.

![Alt text](/images/personal/imageSegmentation.png?raw=true "Tensorboard visualisation of multi-sequence image inputs, target labels and predictions")

# Age regression and sex classification from T1-weighted brain MR images
Two similar applications employing a scalable 3D ResNet architecture learn to predict the subject’s age (regression) or the subject’s sex (classification) from T1–weighted brain MR images from the IXI database. The main difference between this applications is the loss function: While we train the regression network to predict the age as a continuous variable with a L2-loss (the mean squared differences between the predicted age and the real age), we use a categorical cross-entropy loss to predict the class of the sex.

![Alt text](/images/personal/ageRegression.png?raw=true "Example input T1-weighted brain MR images for regression and classification")

# Representation learning on 3T multi-channel brain MR images
Here we demo the use of a deep convolutional autoencoder architecture, a powerful tool for representation learning: The network takes a multi-sequence MR image as input and aims to reconstruct them. By doing so, it compresses the information of the entire training database in its latent variables. The trained weights can also be used for transfer learning or information compression. Note, that the reconstructed images are very smooth: This might be due to the fact that this application uses an L2-loss function or the network being to small to properly encode detailed information.

![Alt text](/images/personal/representationLearning.png?raw=true "Test images and reconstructions using a deep convolutional auto-encoder network")

# Simple image super-resolution on T1w brain MR images
Single image super-resolution aims to learn how to upsample and reconstruct high-resolution images from low resolution inputs. This simple implementation creates a low-resolution version of an image and the super-res network learns to upsample the image to its original resolution (here the up-sampling factor is [4,4,4]). Additionally, we compute a linearly upsampled version to show the difference to the reconstructed image.

![Alt text](/images/personal/imageSuperresolution.png?raw=true "Image super-resolution: original target image; downsampled input image; linear upsampled image; predicted super-resolution;")