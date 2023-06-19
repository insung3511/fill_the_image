Github Link: [https://github.com/insung3511/fill_the_image](https://github.com/insung3511/fill_the_image)

# Fill the Image (with Convolution Embedding)

Author: InSung Bahk, Jehyun Park, Seonghyeon Lim (Major of Artificial Intelligence Convergence in Hallym University)

Our project aims to restore an image by generating a new image from a masked image. In previous research and projects, GANs were commonly used to improve performance. However, they have drawbacks such as long training times and conceptual difficulties. To address these issues, we improved and enhanced the approach by constructing an Autoencoder model with convolution layers. We used the U-Net architecture to form the Autoencoder and applied ResNet's BottleNeck to each layer to enhance the model's performance.

## Introduction

Previous research has explored models that generate new content in the masked regions of an image. Many of these models are based on generative artificial intelligence techniques like GANs [[1]](https://www.semanticscholar.org/paper/Image-Adaptive-GAN-based-Reconstruction-Hussein-Tirer/944d54502895811d3b2c72d1a1d49a395588f67e) [[2]](https://www.mdpi.com/2073-8994/12/3/449) [[3]](https://link.springer.com/article/10.1007/s10489-022-03577-2). While recent approaches have used attention mechanisms to improve performance and restore images, they often require complex preprocessing steps such as patch-based division for image recognition. In our project, we implemented image restoration using a basic model from Vision Deep Learning: the Autoencoder.

## Background

One of the most well-known Autoencoder architectures in vision and imaging is the U-Net [[4]](https://arxiv.org/abs/1505.04597). Although U-Net was initially introduced for image segmentation, we consider it as an Autoencoder architecture. We adopted the U-Net model initially with GoogLeNet's Inception V3 in each layer [[5]](https://arxiv.org/abs/1409.4842). However, due to limited computing resources, we chose a simpler and more improved module. Among several options, we decided to utilize ResNet's BottleNeck [[6]](https://arxiv.org/abs/1512.03385v1) because it exhibits good performance despite its shallow and straightforward structure. Additionally, it was well-suited for our available computing resources.

Existing research focuses more on the model's structure and techniques rather than preprocessing the dataset. We made efforts to propose a lightweight model and explore a simple yet effective method for training data.

## Training Datasets

We utilized the ImageNet dataset [[7]](https://arxiv.org/abs/1409.0575) and Coco Datasets [[8]](https://arxiv.org/abs/1405.0312) as our training datasets for artificial intelligence. Among them, we selected the Coco dataset due to its diverse image types and the presence of multiple metadata. Due to limited computing resources, we randomly extracted 50 images from the dataset.

For each image, we created 50 duplicates, and each duplicate had a different masked image applied as the X data for the model. To address potential overfitting issues, we hypothesized that training on multiple image duplicates would allow the model to extract features effectively, enabling it to learn and reconstruct various characteristics such as forests and animals from the background image. The y data consisted of the original images with the random masks removed, resulting in X data with random masks and y data without masks. All

 images were resized to 256x256x3 dimensions.

## Modeling

We applied the concept of skip connections from U-Net to connect the output feature maps of the BottleNeck blocks with their respective input feature maps. This formed our model architecture as follows:

![Our Model](./model.png)

The skip connections of the BottleNeck blocks were connected in a U-Net-like manner. While the overall structure is similar to U-Net, each convolution layer is in the form of a BottleNeck block. The encoder channel sizes are 3, 64, 128, and 256, and the latent space has a channel size of 512. The decoder channel sizes are the reverse of the encoder: 256, 128, 64, and 3.
