# Semantic segmentation of Salt deposits using UNet

## Semantic Segmentation
The goal of semantic image segmentation is to label each pixel of an image with a corresponding class of what is being represented. Because we’re predicting for every pixel in the image, this task is commonly referred to as dense prediction.
The output itself is a high resolution image (typically of the same size as input image) in which each pixel is classified to a particular class. Thus it is a pixel level image classification.

## Dataset
Link : https://www.kaggle.com/c/tgs-salt-identification-challenge/data

In the images directory, there are 4000 seismic images which are used by human experts to predict whether there could be salt deposits in that region or not.
In the masks directory, there are 4000 gray scale images which are the actual ground truth values of the corresponding images which denote whether the seismic image contains salt deposits and if so where


<img width="722" alt="Screenshot 2022-09-06 at 8 39 09 PM" src="https://user-images.githubusercontent.com/54216044/188670863-f6700c43-5bc3-420a-af4e-d62bbc45e7b6.png">

## Model = UNET
 The architecture contains two paths. First path is the contraction path (also called as the encoder) which is used to capture the context in the image. The encoder is just a traditional stack of convolutional and max pooling layers. The second path is the symmetric expanding path (also called as the decoder) which is used to enable precise localization using transposed convolutions. Thus it is an end-to-end fully convolutional network (FCN), i.e. it only contains Convolutional layers and does not contain any Dense layer because of which it can accept image of any size.
 
 <img width="701" alt="Screenshot 2022-09-06 at 8 40 39 PM" src="https://user-images.githubusercontent.com/54216044/188671165-0f5a46be-605c-47d9-8eb1-8d531fd8cc97.png">

## Training 
Adam Optimizer and Binary Cross Entropy used
Learning rate decay if the validation loss does not improve for 5 continues epochs.
Early stopping if the validation loss does not improve for 10 continues epochs.
Save the weights only if there is improvement in validation loss.
