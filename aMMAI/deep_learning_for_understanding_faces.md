# Deep Learning for Understanding Faces
*Machines may be just as good, or better, than humans*


## Introduction

Deep convolution neural networks (DCNNs) has shown impressive performance on computer vision problems, due to the availability of large annotated data and power computation (GPUs). This article focuses on discussing facial recognition and related problem involving DCNNs.

## Method

1. *Face Detection in Unconstraed Images*
- Traditional method
	- Feature extraction (e.g.Haar wavelets, HOG ...) + Classifier (e.g. SVM)
	- Features do not capture salient facial information at different conditions
- DCNN
	- Region based: R-CNN family
		- Low recall due to region proposal on hard faces
		- Addition computation on proposal generation 
	- Sliding-window based: Single-shot detector (SSD)

2. *Finding Crucial Facial Keypoints and Head Orientation*
- Model based: AAM, ASM, and CLM
	- Lack the power to capture complex face image variations
	- Sensitive to initialization in gradient descent optimization
- Cascaded regression based
	- Multitask learning (MTL): build synergy and learn robust feature

3. *Face Identification and Verification*
- Robust feature learning
	- Learning invariant and discriminative features
	- Metric learning: Siamese, Triplet, Center loss
- Training Datasets
	- Still-images / Video
	- Celebrity faces: large, easy to collect, but noisy

4. *Facial attributes*
- Identify facial attributes (soft biometrics) from single face

5. *MTL for facial analysis*
- JointCascade, HyperFace, TCDCN, All-in-One Face

## Results

1. Introduced crucial problems related with face analytics and recent methods
2. *Open issues*
	- Face detection in wide range of variation in appearance
	- Which layer corresponds to local features for fiducial detection
	- How to choose informative pairs or triplets for training
	- Video-based face analytics

## Discussion

1. Big data and computation power made DCNN possible, it has shown that DCNN is more robust to variations of face apperance due to end-to-end training and wide range of data
2. We use large datasets collected from the internet to evaluate results of the methods, many work show superhuman performances on the datasets, however, these datasets might not meet reality conditions, we should be careful interpreting the results
3. Multitask learning helps learning more robust and discriminative features
4. Training on still image and transfering to video performs worse, which is expected
5. Training with both still image and video jointly performs better than training solely on video, showing that training with wider data is better than deeper data, this is unexpected, might be due to insufficient (in variation) data?
6. Training with label noise hurts the performance, which is a problem that these kind of problems have to face, due to data collected from the internet. Some work uses golden label (checked by human) to perform automatic label correction, which could help to denoise labels
7. Last week, we've seen a work discussing about pre-training on ImageNet, here in face analytics, pre-training seems to be a common technique to get robust and discriminative features, I wonder if the claims from "Rethinking ImageNet Pre-training" still applies to complex problems like face recognition