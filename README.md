# Coding_Drill_Down_MNIST

Modified the code given in the colab file, [MNIST Code](https://colab.research.google.com/drive/1uJZvJdi5VprOQHROtJIHy0mnY2afjNlx) to achieve 99.4% accuracy with less than 20k parameters.

# How the problem was approached

* Skeleton - Reduced the number of parameters using Convolution Blocks with less number of output channels (removed 64, 128, 256 and 512 for every layer) and removed bias
* Max-Pooling - Transition Block (max pooling followed by 1x1) after 5x5 receptive field added in network.
* Batch-Normalization - Added after every convolution layer except the last one to normalize the values being passed between convolution layers
 * Capacity - With very less paramters ~4k parameters, even with all the right concepts in place model couldnt learn. Increased capacity a bit to increase the accuracy.
* Global Average pooling - GAP followed by fully connected layer (1x1 is applied on 1d data) used just before prediction to give the network a little flexibility with the input image size.
* Augmentation - Image augmentation technique like image rotation, color jitter and affine transformation are used
* Regularization - Adding drop out, helped reduced the gap between training and test loss.
* Learning Rate - Used OneCycleLR Learning Rate to tune the model

# Statistical Analysis

| Experiment | Target | Parameters | Train Accuracy | Test Accuracy | Analysis|
| --------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | ----------------- | ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [MNIST\_Basic\_Setup](https://github.com/harshvs4/Coding_Drill_Down_MNIST/blob/main/Exp1_Skeleton.ipynb) | • Get the set-up right<br>• Set Transforms<br>• Set Data Loader<br>• Set Basic Working Code<br>• Set Basic Training & Test Loop| 6,379,786| 99.93 | 99.28|• The Model is extremely heavy with over 6 million parameters<br> • Model is overfitting but this problem will be dealt with in the next step|
| [MNIST\_Less\_Params](https://github.com/harshvs4/Coding_Drill_Down_MNIST/blob/main/Exp2_LessParams.ipynb) | • Reduce the number of input and output channels<br> •Add a transition block with 1x1 pooling | 4,572 | 98.14 | 98.23 | • The model is more structered now<br> • The performance has reduced in comparison to previous mode and this is because of the reduced number of parameters|
|[MNIST\_Batch\_Normalization](https://github.com/harshvs4/Coding_Drill_Down_MNIST/blob/main/Exp3_batch_normalization.ipynb) | • Added Batch Normalization after every convolution and ReLU layer| 4,652 | 99.20 | 98.80 | •  There is slight increase in the number of parameters, as batch norm stores a specific mean and std deviation for each layer<br> • Model overfitting problem is rectified to an extent. But have not reached the target test accuracy 99.40%.|
|[MNIST\_Dropout](https://github.com/harshvs4/Coding_Drill_Down_MNIST/blob/main/Exp4_dropout.ipynb) | • Added dropout of 0.2 after every batch normalization layer | 4,708 | 97.83 | 98.52 | •  There is no overfitting at all. With dropout training will be harder, because we are droping the pixels randomly.<br>•  The performance has droppped, we can further improve it.|
|[MNIST\_Fully\_Connected\_Layer](https://github.com/harshvs4/Coding_Drill_Down_MNIST/blob/main/Exp5_FC_layer.ipynb) | • Increase model capacity at the end | 6,124 | 99.08 | 99.21 | • The model parameters have increased<br>• There is no overfitting rather slight underfitting, thats fine dropout is doing its work , because we are adding dropout at each layer the model is able to capture the training accuracy|
|[MNIST\_Augmentation\_Layer](https://github.com/harshvs4/Coding_Drill_Down_MNIST/blob/main/Exp6_augmentation_layer.ipynb) | • Added augmentation to the image such as Random Rotation, Random Affine and Color Jitter | 6,124 | 97.67 | 99.39 | • The number of parameters remain same<br> • The model is underfitting|
|[MNIST\_LR\_Scheduler](https://github.com/harshvs4/Coding_Drill_Down_MNIST/blob/main/Exp7_GAP.ipynb) | • Added OneCycleLR scheduler<br> • Learning rate scheduler seek to adjust the learning rate during training by reducing the learning rate according to a pre-defined schedule| 7,364 | 98.31 | 99.42 | •The model parameters have increased<br>• Able to achieve 99.4+% accuracy in the last three epochs|
