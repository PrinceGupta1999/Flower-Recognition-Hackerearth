# Flower-Recognition-Hackerearth

## Introduction

This project represents my submission for the [Hackerearth Garden Nerd Competition](https://www.hackerearth.com/challenges/competitive/garden-nerd-data-science-competition). The model uses an ensemble of 4 models all trained through transferred learning and built using the FastAI library.
The models used were:

* Resnet50
* Resnet152
* Densenet121
* Densenet201

Finally the predictions from all 4 models were summed and the prediction with the maximum probability was chosen as overall prediction.

## Feature Engineering

Since the images were the only independent variable in the dataset, there was not much feature engineering to do. However, on observation it was found out that the classes in the training set were highly imbalanced, with dominating class having ~500 examples and dominated class having ~90 examples. To deal with this problem a weighted loss function(NLLLoss) was used for training of the various models. Also as imagenet dataset was trained on 224*224 pixel images, the training images were also shrunk to get full advantage from transfer learning. For generalising better many augmentations were used on the training data including rotations, zooming, cutouts.

## Training

To allow each models to reinforce each other each model was trained by a separate random 60 - 40 training-validation split, thus allowing each model to learn slightly different things from the dataset. After learning on their particular training datasets each model was trained finally on the complete dataset with a very low training rate to allow models to capture more features.
