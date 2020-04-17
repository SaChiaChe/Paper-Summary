# Robust Sparse Coding in Face Recognition

## Introduction

Sparse representation based classification (SRC) has been successfully used in face recognition. These sparse coding models usually assumes that the coding residual follows Gaussian or Laplacian distribution, which might not be realistic. This paper proposes a new scheme, robust sparse coding (RSC), which seeks for the MLE solution for problem, and is more robust to outliers. An efficient iteratively reweighted sparse coding algorithm is also proposed to solve the RSC model.

## Method

1. *The RSC Model*
- Traditional sparse coding problem (LASSO problem)
	- $\min\limits_{\alpha}||y-D\alpha||^2_2\space \text{ s.t. }\space||\alpha||_1\leq\sigma$
	- $D$ is the dictionary (training dataset)
- The MLE of $\alpha$ (RSC) can be formulated as following
	- Assume that the coding residuals ($e$) are i.i.d. according to some probability density function $f_\theta(e_i)$
	- Likelihood of the estimator is: $L_\theta(e_1, ..., e_n)=\prod\limits^n_{i=1}f_\theta(e_i)$
	- Let $\rho_\theta(e_i)=-\ln f_\theta(e_i)$, maximize likeihood becomes minimizing 5h3 object function: $-\ln L_\theta=\sum\limits^n_{i=1}\rho_\theta(e_i)$
	- With consideration of sparsity constraints, RSC can be formulated as $\min\limits_\alpha\sum\limits^n_{i=1}\rho_\theta(e_i)\space\text{ s.t. }||\alpha||_1\leq\sigma$
- Distribution induced weights
	- Approximate RSC with: $\min\limits_\alpha||W^\frac12e||^2_2\text{ s.t. }||\alpha_1||\leq\sigma$ $\Rightarrow$ A weighted LASSO problem
	- $W$ is diagonal with $W_{ii}=w_\theta(e_{0,i})=\rho^{'}_\theta(e_{0,i})/e_{0,i}$
	- Choose logistic function as the weight function, since it has properties similar to AVM's hinge loss: $w_\theta(e_i)=\exp(\mu\delta-\mu e_i^2)/(1+\exp(\mu\delta-\mu e_i^2))$
	- $\rho_\theta(e_i)=\frac{-1}{2\mu}(\ln (1+\exp(\mu\delta-\mu e_i^2)))-\ln(1+\exp(\mu\delta))$
2. *Algorithm of RSC*
- Initialize $y_{rec}$ as mean of all training image and iterate the following algorithm until converge or maximum number of iterations reached
a. Compute residual $e^{(t)}=y-y_{rec}$
b. Estimate $w_\theta(e_i^{(t)})$ with formula induced above
c. Solve the approximated RSC
d. Update sparse coding coefficients
e. Compute reconstructed test sample $y_{rec}^{(t+1)}=D\alpha^{(t+1)}$

## Results

1. *Face Recognition without occlusion*
- Outperforms SRC and other popular mehods (NN, NS, SVM) in most cases on *Extended Yale B database*, *AR database*, and *Multi PIE database*

2. *Face Recognition with occlusion*
- *Pixel Corruption*: 
	- All perform well when only 10% ~ 60% pixel are corrputed
	- RSC has advantage when over 60% of pixels are corrupted
- *Block Occlusion*:
	- RSC achieves much higher recognition rate when occlusion percentage is over 30%
- *Real Face Disguise*
	- Performs a lot better than SRC and Gabor-SRC in all cases

## Discussion

1. They compared result with SRC and a recently (back then) deveploed Gabor-SRC, and in some cases, Gabor-SRC performs better than RSC, maybe they could try integrating Gabor and their method?
2. The sparse coding ideas could be easily merged into deep learning frameworks by adding a L1 regularization term
3. The experiments in this paper uses PCA (eigenface) to first reduce the dimensionality of the origin image, would it still work if other (non-linear) dimesion reduction method is applied ?