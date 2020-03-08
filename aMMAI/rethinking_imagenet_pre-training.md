# Rethinking ImageNet Pre-training

## Introduction

Pretraining on large scale data sources (eg. ImageNet) has been very important in machine learning and computer vision. However, pretraining a 'universal' feature representation with these large scale data is open to doubt. This paper questions the paradigm of pre-training even further by exploring the opposite regime: we could reach the accuracy of pre-trained model with random initialization.

## Method

They conducted several experiments to compare random initialized model (trained from 'scratch') and ImageNet pre-trained model. 
To better understand what impact the ImageNet could make, only minimal modification were made to enable typical architectures to be trained from scratch.
1. *Normalization*
	- Small batch sizes degrades the accuracy of Batch Normalization (**BN**)
	- *Group Normalization* (**GN**) and *Synchronized Batch Normalization* (**SyncBN**) is used
	- With appropriate initialization, it is possible to train without BN or GN
2. *Converence*
	- It is unrealistic to expect training from scratch could converge as fast as those pre-trained from ImageNet
	- They argue that model trained from scratch must be trained for longer
	- This is a *fairer* comparison in terms of the number of training samples provided

## Results

The main observation are as follows:
1. Training from scratch is possible without architecture change
2. Training from scratch requires more iterations to converge
3. Training from scratch can be no worse than pre-trained on ImageNet under many circumstances, down to as few as 10k COCO images
4. ImageNet pre-training speeds up convergence
5. ImageNet pre-training does not necessarily help reduce overfitting unless insufficient data
6. ImageNet pre-training helps less if the target task is more sensitive to localization than classification

## Discussion

1. ImageNet pre-training might not be necessary if we have enough data, however, it still helps speeding up convergence and avoids overfitting when insufficient data
2. The paper claims that with proper initialization, training from scratch could reach the same accuracy as pre-trained from ImageNet. However, the experiments are conducted on well known open source data, optimal initialization and hyper-parameter tuning might be difficult in real tasks.
3. Real world applications often face a problem: insufficient data. Thus, pre-training on large scale data source such as ImageNet is still a good option when getting sufficient annotated data is not available