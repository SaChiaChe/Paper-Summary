# FaceTracer: A Search Engine for Large Collections of Images with Faces

## Introduction

This paper creates a image search engine based entirely on faces. Using a novel combination of SVM and adaboost which exploits strong structures of faces to select features. The framework is fully automatic, easy to scale, and computes all labels off-line, leading to fast on-line search performance.

## Method

1. *Creating the Face Database*

![](./figure/facetracer-a_search_engine_for_large_collections_of_images_with_faces.png)

2. *Automatic Attribute Classification for Face Images*

- Face Regions, Types of pixel data, Normalization, Aggregation
- First train SVMs on local features (*Attribute-Tuned Local SVMs*)
	- Since features are either powerful or useless, retraining will not improve too much
	- Only train SVMs once, then use adaboost to obtain the weights
- Then train a SVM on top of the features from the top classifiers selected by adaboost (*Attribute-Tuned Global SVM*)

## Results

Search example:

![](.//figure/facetracer-a_search_engine_for_large_collections_of_images_with_faces_result1.png)

Comparison to other methods:

![](.//figure/facetracer-a_search_engine_for_large_collections_of_images_with_faces_result2.png)

## Discussion

1. The use of SVM and adaboost is very innovative, adaboost is a very powerful tool for classifiers, which could be implemented over any classifier
2. Only training the SVMs once is a great idea, spotting out that retraining might not change much, and could improve speed a lot
3. Google image search improved a lot from the days of this paper (the search results are super relevant now), wonder if google did something to improve image feature rather than simply using text retrieval methods
