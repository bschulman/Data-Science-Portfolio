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

The final model is a sequential convolutional neural network (CNN) with the following architecture:

Four convolutional blocks with maxpooling.

Three dense layers with 128 neurons each. 

Relu activation and he-normal initialization

The last dense layer has 3 neurons and softmax activation. 

The model is compiled with Adamax optimizer and categorical_crossentropy loss and accuracy, recall, precision and AUC as metrics.

I also use a custom cyclical learning schedule to increase and then reduce the learning rate for each training cycle to prevent overfitting.

**Results:**
I was ultimately unable to train a classifier that could distinguish between the sad and neutral classes. However, I was able to train a highly accurate classifier that could distinguish between a combined sad-neutral class, happy, and surprise.

On that classifier, I acheived a validation accuracy of about 88% and a .96 AUC and a test accuracy of 92% a .973 AUC.

Usage
Code requires: zipfile, matplotlib, numpy, pandas, cv2, tensorflow, keras, tensorflow add ons, scikitlearn. It was written in colab so it imports the data from Google Drive

