# Style Transfer + VAE+ Supervised Learning
# Summary of the proposed Network
## Purpose
The proposed VAE + Style Transfer + Supervised Learning Network is trained to help us to predict material properties of interest. Since standard CNN network(VGG or Alex Net) could be used to predict material properties of interest such as Young's Module, Diffusion coefficient with high accuracy in ordinary value, but low accuracy at some extreme values. The problem is that the material microstructures with extreme properties are always hard to generate through traditional method, which makes the training data short of these extreme cases. The network could help us generate these types of samples that could be used to address the issue gradually. 

![](image/Recon.JPG)

![](image/Random.JPG)

![](image/Change.JPG)

## Model
We set up a 16-layer VAE network + a 4-layer Style Transfer network.

![](image/Model.JPG)

### detail parameter
- VAE:

![](image/VAE.JPG)

- Style Transfer: 

We use the first 4 layers from the pretrained VGG network, due to our image size is 128 by 128.
This number could be adjusted based on your input size.

- Error Term:

In this case we have 4 error terms: (a)Reconstruction Error, (b)KL-Divergence Error, (c)Model Collapse Error, (d)Style Transfer Error and (e) Regression Error.
Error (a)(b) are traditional error terms for VAE; Error (c) is used for preventing model from collaps(Please refer to the paper [Improved GAN](https://arxiv.org/abs/1606.03498)
for technique detail; Error (d) is the difference between Gram matrix from input samples and generated images(in our case, we randomly pick; Error (e) is the difference between true value and predicted value, noticed that multiple regression network could be applied to predict different properties.
a batch from 20 out of 780 input samples in every epoch as comparing target), please refer to [Style Transfer](http://www.cv-foundation.org/openaccess/content_cvpr_2016/html/Gatys_Image_Style_Transfer_CVPR_2016_paper.html)
for techique detail.

## Prerequisites for Running the code
### Package
- Cuda >= 6.5
- Python = 3.5
- Tensorflow >= 1.0
- Keras latest version
- h5py

### Download
Please download VGG pretrained weights from [https://github.com/fchollet/deep-learning-models/releases](https://github.com/fchollet/deep-learning-models/releases)

