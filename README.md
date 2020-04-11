# 11717701_KM030_26_Ashish-kumar-Satellite-farming-using-remote-sensing-images-drone-images-
Get Input Data The input data was encoded into CSV files. The X_test_sat4.csv flattened the images that were 28 x 28 x 4 that were taken from space. The first three channels are the standard red, green, and blue channels in normal images. The 4th is a near-infrared band. We are using the smaller test set because the training set is too big. After extracting the data from the csv files, we can reshape it into the original images. Then, we can see the images before we train on them. The second file we are loading are the labels for each image. They can be one of 4: barren land, trees, grassland and other. Each row in the file looks like this [1,0,0,0], where only one of the 4 value is 1. If it is one, then it is that class respective to the order I showed above. If it was the above values, the image is a picture of barren land. If it was [0,1,0,0], then it would be trees. If it was [0,0,1,0], then it would be grassland and so on.
Let's now define our model
There are 2 different types of models we can choose from: A 'vanilla' artificial neural network we have been learning about, and a special Convolutional Neural Network we will learn about, which is very, very good at image recognition. For now we will use the simpler, vanilla artificial neural network. The network will only have one layer: the output one. This network will not be expected to be very powerful, and pretty slow.

In [6]:

model = Sequential([

    Dense(4, input_shape=(3136,), activation='softmax')

])



Now that we have the data and model ready, there is one more thing we have to do. In neural networks, it is very important we normalize training data. This means we make the mean 0, and the standard deviation 1 for the best results. However, dividing the image by 255 is good enough. We will just divide the array by 255:

X_train = X_train/255



Now lets fit our model to the training data
In [8]:

model.compile(optimizer='adam', loss='categorical_crossentropy', metrics=['accuracy'])

model.summary()

model.fit(X_train,Y_train,batch_size=32, epochs=5, verbose=1, validation_split=0.01)

