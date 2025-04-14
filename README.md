In this assignment we trained and evaluated three different CNN architectures on CIFAR10: 
We designed 2 variations of the LeNet5 architecture, which we believed would improve performance. 

1) CIFAR10_lenet: simple LeNet5
2) CIFAR10_model1: LeNet5 + BatchNorm
3) CIFAR10_model2. LeNet5 + BatchNorm + Dropout

We use early stopping, learning rate scheduling, pretraining, saving and transfering weights and data augmentation.
For training we used CE loss and Adam optimizer. Initial learning rate was set to
CIFAR10_model2 had the best results in our runs, although CIFAR10_model1 was very close.
Next, we use CIFAR100's 20 superclasses (coarse labels) to train the best architecture from scratch (CIFAR10_model2) on this new classification problem.
To implement this, we had to change the size of the output layer. After training, on the coarse labels of CIFAR100, we get CIFAR100_model.
Then we transfer CIFAR100_model weights (or just change the output layer back) and then train on CIFAR10 again. This is how we get CIFAR10_pretrained.
Finally, we evaluate CIFAR10_pretrained and CIFAR10_model2 on CIFAR10's test data and compare their performance.  

As an additional task we evaluate the architecture's cross-dataset performance on TinyImagenet's overlapping classes.
At first we test the best architecture on new dataset and later, we finetune on it and test the finetuned model.

We provide the weights of all the trained models after the last epoch of their training.
train_model() function implements the training procedure and outputs the resulting loss and accuracy plots, 
as well as a plot of the learning rate over the training epochs. 
During testing we calculate the accuracy and the confusion matrix.
