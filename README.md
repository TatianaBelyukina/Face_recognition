# Face_recognition
# Siamese neural network

A Siamese neural network is a class of neural network architectures that contain two or more identical subnetworks. "identical" here means that they have the same
configuration with the same parameters and weights. The parameter update is reflected in both subnets. It is used to find similarities in input data by comparing feature vectors, so these networks are used in
many programs. Traditionally, a neural network learns to predict several classes. This creates a problem when we need to add/remove new classes to the data. In this case, we have to update the neural network and retrain it on the entire data set. In addition, deep neural networks require a large amount of data for training. SNNs study the similarity function. So we can teach her to see if two images are the same. This allows us to classify new classes of data without retraining the network.

# The first stage is dataset collection.
Using the python programming language and the built-in opencv library, I wrote a script that helped me take photos using a web camera on a laptop. With the help of the face_recognition library, I cropped the photo so that there were as few extra objects in the image as possible. Thus, I collected 20 photos of 5 of my acquaintances.

And it seems that you can start processing the date and building a convolutional neural network, but after taking all the steps that will be described below, I received strong retraining (in training, the accuracy was 0.95, and in the test, 0.51), this is understandable, because this dataset is very bad for training, it is likely that the neural network learned to recognize not the face, but the background, lighting, etc. Therefore, I decided to change the approach to creating a dataset. This time I took a photo from shared access - Instagram and, just like with the previous dataset, cropped the face using the face_recognition library. This approach had 2 advantages over the past:
- The size of the dataset will be much larger, because it is much easier to collect photos of people. And the more data, the better the quality of the neural network
- Photos of the same person were taken at different times, in different places, with different lighting, so the neural network will learn to recognize the face itself

- In this way, I collected +-20 photos of 21 different people, since the library does not always correctly find faces, so in some cases the number of photos is less. Next, I combine these images into a dataset using the tensorflow library. How
is the dataset being formed? I combine each input image with a positive (same person as in the input photo) and a negative (different person from the person in the input photo) image and add a label, 1 = positive feedback, 0 = negative.

By forming such pairs for each person, I got a dataset of size 812. In general, photos are stored as arrays of size: width x height x 3
Next, I process each photo - reshape each image to 100x100x3 so that all photos are the same size, and normalize the pixel values - divide the value of each pixel by 255, so instead of values 0 - 255, we got arrays with values 0 - 1. The next step I split the dataset into train(70% of data) and test(30% of data) and define an architecture for a convolutional neural network.
