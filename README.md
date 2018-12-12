# README

This repository contains information and code on how to create Stylized-ImageNet, a stylized version of ImageNet that can be used to induce a shape bias in CNNs as reported in our paper "ImageNet-trained CNNs are biased towards texture; increasing shape bias improves accuracy and robustness" by Robert Geirhos, Patricia Rubisch, Claudio Michaelis, Felix A. Wichmann, Wieland Brendel, and Matthias Bethge. We hope that you may find this repository a useful resource for your own research.

Please don't hesitate to contact me at robert.geirhos@bethgelab.org or open an issue in case there is any question!

The code itself heavily relies on the [pytorch-AdaIN github repository](https://github.com/naoto0804/pytorch-AdaIN) pytorch-AdaIN github repository, which is a PyTorch implementation of the AdaIN style transfer approach by X. Huang and S. Belongie, "Arbitrary Style Transfer in Real-time with Adaptive Instance Normalization.", published at ICCV 2017. In fact, the entire AdaIN implementation is taken from this repository; in order to enable anyone to create Stylized-ImageNet with as little additional effort as possible we here make everything available in one repository (preprocessing, style transfer, etc.).

## Example images
Here are a few examples of how different stylization of the same ImageNet image can look like:
![](./example_imgs/example_stylization_imgs.png) 
As you can see, local textures are heavily distorted, while global object shapes remain (more or less) intact during stylization. This makes Stylized-ImageNet an effective dataset to nudge CNNs towards learning more about shapes, and less about local textures.

## Usage
1. Get style images (paintings). Download ``train.zip`` from [Kaggle's painter-by-numbers dataset](https://www.kaggle.com/c/painter-by-numbers/data); extract the content (paintings) into this new directory: ``code/paintings_raw/`` (about 38G).
2. Get ImageNet images & set path. If you already have the ImageNet images, set the ``IMAGENET_PATH`` variable in ``code/general.py`` accordingly. If not, obtain the ImageNet images from the [ImageNet website](http://image-net.org/download-images) and store them somewhere locally, then set the variable. Note that the ImageNet images need to be split in two subdirectories, ``train/`` and ``val/`` (for training and validation images, respectively). In any case, also set the ``STYLIZED_IMAGENET_PATH`` variable (also in ``code/general.py``. This variable indicates the path where you would like to store the final dataset. Make sure you have enough disk space: In our setting, Stylized-ImageNet needs 134G of disk space (which is a bit less than standard ImageNet with 181G).
3. go to ``code/`` and execute ``create_stylized_imagenet.sh`` (assuming access to a GPU). The easiest way for doing this is to the docker image that we provide (see Section below). This creates Stylized-ImageNet in the directory that you specified in step 2.
4. Optionally, delete ``paintings_raw/``, ``paintings_excluded/`` and ``paintings_preprocessed/`` which are no longer needed.

## Docker image
We provide a docker image so that you don't have to install all of the libraries yourself here: [https://hub.docker.com/r/bethgelab/deeplearning/](https://hub.docker.com/r/bethgelab/deeplearning/). The repo is tested with ``bethgelab/deeplearning:cuda9.0-cudnn7``.
