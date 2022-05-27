# Image Colorization

By Daniel Mata, YingHsuan Lo, Naga Sumanth Vankadari

For this project, we decided to tackle the challenge of training a model to colorize black and white photos. For our dataset, we used this landscape dataset from Kaggle. For the architecture of the model, we based it on the CNN model from this paper. We will go through the code and describe the process in detail. To start, the following code demonstrates how we will be working with the LAB colorspace. The input for our model is the L channel, which is the luminance and ranges from 0-100 values. The output for our model are the ab channels, which represent different spectrum ranges (a is red-green, b is yellow-blue) with values ranging from -128-127.

We can see an example of the Lab colorspace right below, in which the Lightness channel is the input and the output is a pair of the two other channels.

![Lab colorspace examples](https://github.com/daniel-m777/image_colorization/blob/main/images/lab%20colorspace.png)

Our model consists of several blocks of CNNs based on the paper mentioned above. However, we converted from PyTorch to TensorFlow code and tweaked a couple of parameters in order to better suit our process. More specifically, we changed our input shape, adjusted padding/strides such the output matched the target data, and switched from a final SoftMax activation to a Tanh, given that we normalized our values to be from -1-1 rather than 0-1 (like in the original paper). Moreover, we used an adam optimizer with a slow learning rate, early stopping, and RMSE and the metric. Overall, our model was a regression task that differed from the paper in which they treated the problem as a classification task.

Below we can see some of the final results from our CNN-based model. First, we observe the best images, in which the desaturated colors are clearly seen being favored (as mentioned in the original paper). Images that were already comprised of mostly blue and white were the most accurate.

![Best images](https://github.com/daniel-m777/image_colorization/blob/main/images/best%20images.png)

In the second set of images, we display the worst predicted images. For images that were mostly green, the images predicted were desaturated as usual. For images with mostly red, however, we see that the colors predicted were almost prevalently green.

![Worst images](https://github.com/daniel-m777/image_colorization/blob/main/images/worst%20images.png)

Finally, we have a single image with okay colorization. To reiterate, the question looks convincing seemingly due to the ground truth being already desaturate, grayish colored.

![prediction](https://github.com/daniel-m777/image_colorization/blob/main/images/prediction.png)

There were a couple more additional observations that we noticed.

- Even though our colors were sometimes very off, both models were still recognizing the shapes and structures within the images.

- Although our models can recognize these shapes and structures, they still confine to the subject matter (in our case landscape images). For example, we tried to colorize human faces and it did not work as well compared to the landscape images.
