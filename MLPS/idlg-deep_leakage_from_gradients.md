# iDLG: Improved Deep Leakage from Gradients

## Introduction

In DLG ([Deep Leakage from Gradients](https://papers.nips.cc/paper/2019/file/60a6c4002cc7b29142def8871531281a-Paper.pdf)), both the data and the target is obtained from optimizing the gradient loss. This work discovered that when using softmax and cross-entropy, the target could be extracted definitely.

## Method

When using softmax and cross-entropy loss, the gradient is negative only on the target label. The derivation process is as the following:

$l(x,c)=-\log\frac{e^{y_c}}{\sum_je^{y_j}}$
$g_i=\frac{\partial{l(x,c)}}{\partial{y_i}}=-\frac{\partial{\log{e^{y_c}-\partial{\log{\sum_je^{y_j}}}}}}{\partial{y_i}}=\cases{-1+\frac{e^{y_c}}{\sum_je^{y_j}}<0, \ \text{ if }i=c\\\frac{e^{y_c}}{\sum_je^{y_j}}\geq0, \ \text{otherwise}}$
$\nabla{W_L^i}=\frac{\partial{l(x,c)}}{\partial{W_L^i}}=\frac{\partial{l(x,c)}}{\partial{y^i}}{\cdot}\frac{\partial{y^i}}{\partial{W_L^i}}=g_i{\cdot}\frac{\partial({W_L^i}^Ta_{L-1})+b_L^i}{\partial{W^i_L}}=g_i{\cdot}a_{L-1}$
$\text{Ground Truth label } c=i,\ s.t.\nabla{W_L^i}^T\cdot\nabla{W_L^j}, \forall{j{\neq}i}$

## Results

<p align="center">
  <img src="./figure/idlg-deep_leakage_from_gradients.png"><br>
</p>

The extracted labels are 100%, while DLG might extract incorrect labels.

## Discussion

1. iDLG converges faster and better since it has the correct target label in hand.
2. This work only works on top of a very restricted assumption, which only works on cross-entropy loss and you have to obtain the gradient for each sample in a training batch, this might not be realistic.