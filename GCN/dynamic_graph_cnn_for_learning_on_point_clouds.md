# Dynamic Graph CNN for Learning on Point Clouds

## Introduction:
This paper presents a novel operation &mdash; Edge Convolution,  for learning from point clouds, to better capture local geometric feature while remaining permutation invariance. It could be easily integrated into multiple existing pipeline for point cloud processing, and achieves state-of-the-art performance on benchmark datasets.

## Method:

![](./figure/dynamic_graph_cnn_for_learning_on_point_clouds_1.png)

1. *Edge Convolution*

![](./figure/dynamic_graph_cnn_for_learning_on_point_clouds_2.png)

- ![](./figure/dynamic_graph_cnn_for_learning_on_point_clouds_equation_1.svg)
	- ![](./figure/dynamic_graph_cnn_for_learning_on_point_clouds_equation_2.svg)
	- ![](./figure/dynamic_graph_cnn_for_learning_on_point_clouds_equation_3.svg)
	- Could be implemented as a shared MLP

## Results:

1. *Part Segmentation*

![](./figure/dynamic_graph_cnn_for_learning_on_point_clouds_3.png)


2. *Indoor Scene Segmentation*

![](./figure/dynamic_graph_cnn_for_learning_on_point_clouds_4.png)


## Discussion:

- ["Rethinking Table Recognition using Graph Neural Networks"](https://github.com/Cinnamon/IDEA_Input/blob/master/INFORMATION_EXTRACTION/rethinking_table_recognition_using_graph_neural_networks.md) uses DGCNN in an elagent way, by recognizing a table with rows, columns, and cell structures.
- How to modify the edge convolution to better capture key-value pairing structure ? 
