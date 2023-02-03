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


**Model:**

The latest model is a sequential convolutional neural network (CNN) with the following architecture:

Four convolutional blocks with maxpooling.

Three dense layers with 128 neurons each. 

Relu activation and he-normal initialization

The last dense layer has 4 neurons and softmax activation. 

The model is compiled with Adamax optimizer and categorical_crossentropy loss and accuracy as the metric.

I also use a custom cyclical learning to increase and then reduce the learning rate for each training cycle to prevent overfitting.

**Results:**
So far, I've acheived a validation accuracy of about 80% and a test accuracy of 57%. However, the model can't distinguish between sad and neutral.

**Next Steps:**
1. Further tune cyclical learning rate.
2. Train the model on just sad and neutral then retrain with all four.

Usage
Code requires: zipfile, matplotlib, numpy, pandas, cv2, tensorflow, keras, tensorflow add ons, scikitlearn. It was written in colab so it imports the data from Google Drive

Note:

This is a work in progress. More updates and improvements are expected.
