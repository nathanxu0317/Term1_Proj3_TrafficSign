# **Traffic Sign Recognition** 

## Writeup

---

**Build a Traffic Sign Recognition Project**

The goals / steps of this project are the following:
* Load the data set (see below for links to the project data set)
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report


[//]: # (Image References)

[image1]: ./Samples.png "Analysis of Training Sample"
[image2]: ./11_Rightofway.jpg "Right of Way"
[image3]: ./12_PriorityRoad.jpg "Priority Road"
[image4]: ./17_Noentry.jpg "No Entry"
[image5]: ./25_RoadWork.jpg "Road Work"
[image6]: ./33_RightOnly.jpg "Right Only"



---
### Writeup / README


### Data Set Summary & Exploration

I used the pandas library to calculate summary statistics of the traffic
signs data set:

* The size of training set is 34799
* The size of the validation set is 12630
* The size of test set is 4410
* The shape of a traffic sign image is 32x32x3
* The number of unique classes/labels in the data set is 43

Here is an exploratory visualization of the data set:

![alt text][image1]

### Design and Test a Model Architecture

#### 1. Preprocess the image data. 

Here only the original data set has been used, data argumentation was not applied.
Color pictures are used as training input instead of grayscaled ones, because the former contains more useful info. 

All data should be normalized to 0 mean & 1 variance, considering numerical stability and efficiency of optimization.


#### 2. Final model architecture 

My final model consisted of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x3 RGB image   							| 
| Convolution 5x5     	| 1x1 stride, same padding, outputs 28x28x10 	|
| RELU					|	Nonlinearization											|
| Max pooling	      	| 2x2 stride,  outputs 14x14x10 				|
| Convolution 5x5	    |  1x1 stride, same padding, outputs 10x10x20	|
| RELU					|	Nonlinearization											|
| Fully connected		| outputs 1*500        									|
| Fully connected		| outputs 1*200        									|
| Fully connected		| outputs 1*43        									|
| Softmax				| outputs Final Propability       									|
|						|												|

The max pooling for second layer was deleted, due to that max pooling would eliminated some useful info.
The number of filters in each layer has been increased, please refer to the above table.
Although the training result is satisfying, this may cause more overfitting problem.

#### 3. Model training

Epochs is set to 50, learning rate is set to 0.001, batch size is set to 128.
Larger epochs will have higher confidence of good result, even a number of 35 epochs was found to be ok.

#### 4. Approach to find the solution   

The LeNet architecture was chosen. It is proven in previous project for detecting info in grayscaled picture. Color picture works similarly.  

As mentioned above, color picture has more info, so grayscaling was not done to the original data set. Then the max pooling of seccond layer has been deleted in order to keep more info. The filter numbers has been increased a little bit in order to get better result.

My final model results were:
* validation set accuracy of 0.946
* test set accuracy of 0.940


### Test a Model on New Images

#### 1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

Here are five German traffic signs that I found on the web:

![alt text][image2] ![alt text][image3] ![alt text][image4] 
![alt text][image5] ![alt text][image6]

The first image might be difficult to classify because the photo is taken at dark light conditions and there is not enought contrast between the sign and background. 

#### 2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. 

Here are the results of the prediction:

| Image			        |     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| Right of way      		| Animals danger   									| 
| Priority Road     			| Priority Road 										|
| No entry					| No entry											|
| Road Work	      		| Road Work					 				|
| Right Only			| Right Only      							|


The model was able to correctly guess 4 of the 5 traffic signs, which gives an accuracy of 80%. This compares favorably to the accuracy on the test set of 94%.


#### 3. Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. 

The final model is very confident about the tested 5 pictures, the probability is very close to 1. Although the model did not give the right prediction result for the first image, it is still very confident with its prediction. 
Model Certainty here is highly related with training epochs, with epochs less than 30, the model feels uncertain about the result, and accuracy also decreased.

| probability			        |     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| 1.      		| Animals danger   									| 
| 1.     			| Priority Road  										|
| 1.					| No Entry											|
| 1. 	      		| Road Work					 				|
| 1. 			| Right Only      							|


