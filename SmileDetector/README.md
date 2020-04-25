# Smile Detector Observations

## Preamble ##
* This project is actually from Coursera's Deep Learning Specialization Course #4 (Convolutional Neural Networks)
   * Please don't sue me Coursera
* Anyway, the point of the project is to train a convolutional neural network in order to tell if someone is smiling (label is 1) or not smiling (label is 0)
* The input image is downsized to 64 by 64 and there are 3 channels (red, green, blue)
* For training, there are 600 examples
* For testing, there are 150 examples

## Findings ##
* When training, in the beginning, it seemed like a smaller network was doing better
   * The original model for this project was Conv --> BatchNorm --> MaxPooling --> Relu --> Flatten --> Fully Connected Sigmoid --> Output
   * The training used for this was 20 epochs of 32 mini-batches
      * This means that there were a total of ceil(600 / 32) * 20 updates, which is 380 
   * This got about 91% accuracy
   * After training twice (40 total epochs), the highest accuracy I found was 97%

* I later created a larger network to see how it would fair
   * This network was:
      * (Conv --> BatchNorm --> MaxPooling --> Relu --> Dropout) * 4 --> Flatten --> Sigmoid
   * This network did astronomically worse. It resulted in about 43.3% accuracy after 20 epochs, BUT with a batch size of 128
   * I continuously retrained and retrained and retrained, but it made no difference
   * This is when I FINALLY realized that by increasing the size of the mini-batch, the network was only updating (600 / 128) * 20 times, which is 100 times - almost 4x less than the original model
   * After figuring this out, I retrained the model with about 80 epochs and achieved results of about 90-96% on the test data
   * I then trained with 100 epochs and a batch size of 256, and got an accuracy on the test set of 93.3% (this is the current model)

## Notes for Future ##
* Next time, save each model to be able to reference them later
* Remember, if you increase the mini-batch size, you most likely must increase the number of epochs 
* Maybe try Stochastic Gradient Descent with the Adam optimizer next time (updates on each training example)
* Try an opitimizer that will decrease the learning rate over time because I noticed that during training, the loss can jump around at the end