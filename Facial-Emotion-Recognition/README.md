**Project Title:** Facial Emotion Recognition

**Problem Statement:**
The goal of this project is to use Deep Learning and Artificial Intelligence techniques to create a computer vision model that can accurately detect facial emotions.

**Data:**
The data set consists of 3 folders, i.e., 'test', 'train', and 'validation'. Each of these folders has four subfolders:
● ‘happy’: Images of people who have happy facial expressions.
● ‘sad’: Images of people with sad or upset facial expressions.
● ‘surprise’: Images of people who have shocked or surprised facial expressions.
● ‘neutral’: Images of people showing no prominent emotion in their facial expression at all.
In total there are 15,000 images that all vary in terms of age, racial and gender makeup as well as clarity, lighting, and facial orientation.


Model
The latest model is a sequential convolutional neural network (CNN) with the following architecture:

This is a model for a convolutional neural network. The model starts with a 2D convolutional layer with 64 filters and a kernel size of (7, 7). 
The activation function used is ReLU, with padding set to 'same' and the input shape is (48, 48, 1). 
This is followed by a max pooling layer with pool size 2x2. 
This is followed by 2 more convolutional layers with 128 filters and kernel size of (3, 3) and ReLU activation, same padding and max pooling layer with pool size 2x2. 
Then there is a convolutional layer with 256 filters and kernel size of (3, 3) and ReLU activation, same padding and max pooling layer with pool size 2x2. 
Then the output is flattened and passed through a series of dense layers with 64 neurons, ReLU activation and dropout with dropout rate set to 0.25. 
The last dense layer has 4 neurons and softmax activation. 
The model is compiled with Adam optimizer and categorical_crossentropy loss and accuracy as the metric.
I also use 'ReduceLROnPlateau' to reduce the learning rate of the optimizer when the validation loss stops improving and 'EarlyStopping' to stop the training when the validation loss stops improving after a certain number of epochs.

**Results:**
So far, I've acheived a validation accuracy of about 70%. 

**Next Steps:**
1. changing model metric to Precision & Recall, ROC-AUC, and F1-Score. 
2. Data augmentation: Generate more data by applying random transformations to the existing data
3. Experiment with different architectures:
    - More & different types of layers (e.g. dropout, batch normalization) 
    - Add attention layers that focus on specific facial features
    - Use pre-trained models: VGG, Inception, etc.
4. Hyperparameter tune: 
    - GridSearchCV, RandomizedSearchCV and/or Bayesian optimization (using Tensorboard) to find the optimal values of hyperparameters to optimize said success metrics on each of the different architectures
5. Ensemble methods: Combine predictions of best architectures

Usage
Code requires: zipfile, matplotlib, numpy, pandas, cv2, tensorflow, keras. It was written in colab so it imports the data from Google Drive

Note
This is a work in progress and is a first draft of the project. More updates and improvements are expected.
