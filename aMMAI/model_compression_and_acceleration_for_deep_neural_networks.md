# Model Compression and Acceleration for Deep Neural Networks

## Introduction

Deep neural networks has received huge success in various tasks, these networks rely on millions or even billions of parameters and availability of strong GPUs. However, in some apllication where hardware are limited, how to compact the model becomes important. In this work, they surveyed model compression and acceleration techniques and classify them into 4 orthogonal categories, describe properties, strengths and drawbacks of each category.

## Method

1. *Parameter Pruning and Sharing*
- Reducing redundant parameters that are not sensitive to the performance 
- Quantization and Binarization
    - Reduce number of bits to represent each weight
- Pruning and Sharing
    - Remove redundant weights/connections
    - Sparsity constraints (L1 loss)
- Design structural matrix
    - Use structural matrix to reduce (share) parameters 

2. *Low-Rank Factorization*
- Simplifying the convolution layer to reduce computation
- Discrete cosine transform (DCT), canonical polyadic (CP) decomposition,batch normalization transoformed activation

3. *Transferred/Compact Convolution Filters*
- Apply transformation on layers to a small set of base filters
- Negation transformation, multibias transform, rotation/flipping trnsform

4. *Knowledge Distillation (KD)*
- Train smaller student network guided by a bigger and stronger teacher network
- FitNets, Monte Carlo teacher

## Results

1. *Parameter Pruning and Sharing*
- Robust to various settings, can acheive good performance
- Reduce network complexity and avoid overfitting
- Quantization and Binarization
    - Binary nets significant lowers performance 
- Pruning and Sharing
    - Pruning with L1 or L2 regularization requires more iterations to converge
    - Fine-tuning might be cumbersome 
- Design structural matrix 
    - Constraint might be bias to model
    - Designing structural matrix is hard

2. *Low-Rank Factorization*
- Standarized pipeline, easy implementation
- Usually approximated layer by layer and thus cannot acheive global parameter compression
- Extensive model retraining

3. *Transferred/Compact Convolution Filters*
- Dependent on application, only supports training from scratch
- Strong on wide/flat architectures, but weak on narrow/special ones
- Transfer assumption sometimes too strong to guide the algorithm, resulting in unstable performance

4. *Knowledge Distillation (KD)*
- Model performances are sensitive to applications and network structure
- Can only appy on classification tasks with softmax loss
- Assumptions sometimes are too strict to make the performance competitive with other types of approaches

## Discussion

1. The catogories are orthogonal, thus we could apply multiple methods to get more compression
2. Some methods work like regulizers, and could acheive higher performance than origin network after compression sometimes
3. Could combine learning-to-learn methods to learn how to prune the model