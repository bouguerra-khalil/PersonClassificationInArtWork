

<h1 style="text-align:center">Person Clasification In Artwork Challenge</h1>

## Goal of the challenge 
Artworks such as paintings give us important clues about how people were perceived over centuries in the Western culture, for instance. Building a system that allows scholars to automatically find people in large database of paintings can help art historians and historians to analyse and study how the human representation changed over time (clothes, objects depicted etc.). 
The goal of this challenge is to classify artwork images as containing a person or not. 

## DataSet 

We will use a data-set of 10.000 RGB images of artworks. Data has already been randomly split into a training-validation set (50%) and a test set (50%). we only have the classification of the training-validation set. The goal of the project is to estimate the correct class (person or not) for the test set.

## Data Description 
- folder im : It contains 10000 images of artworks images.
- train.csv : The training set file. It contains the name of the images and their classes: 
	- 0 for no person 
	- 1 for person.
- test.csv  : The test set file in the format you should use for submission.

## Workflow  
- Data Loading 
- Data Preprocessing: 
	- resizing images 
	- converting images ( due to meemry limits we had to convert the images )
	- reshaping the images  
	- Scalling the data 
	- Shuffling 
- Classification Using From Scratch CNN Models
	- Adding Dropout layers to avoid overffiting  
	- Adding Batch Normalization layer to avoid overffiting
- Classification Using Transfer Learning: 
	- Xception
	- InceptionV3
	- InceptionResNetV2
	- VGG16
	- VGG19
	- MobileNetV2
	- ResNet50
	- ResNet101
	- ResNet152
	- ResNet50V2
	- ResNet101V2
	- ResNet152V2
	- MobileNet"
	- DenseNet121
	- DenseNet169
	- DenseNet201
	- NASNetLarge
	- NASNetMobile
- Classification Using INCEPTION pretrained model  from  GOOGLE 
	- adding Callbacks: 
		- EarlyStoping(Avoid overffiting and saves time)
		- ModelCeckPoint(Saves the best model over the training epochs)
		- LearningRateScheduler( to control how much update the weights gets )
	- Overfitting Fix: 
		- Adding Dropout layers to avoid overffiting  	
		- Adding Batch Normalization layer to avoid overffiting
- Data Augmentation  for Data Imbalance fixing


## Results
	
- Classification Using From Scratch CNN Models: 

||Bare Model| |Adding Dropout Layer||
:------------:|:------:|:---------:|:------:|:---------:
|	  |  Train  | Test |  Train  | Test
loss |     0.0045 | 2.1274| 0.069 |  0.720
accuracy | 0.9994  |0.6893 | 0.981 | 0.717

		-> We can notice that the result improved by using the batch normalization and dropout layer, yet we still suffer from the overfitting, which is a very common phenomena when it comes to neural networks, because they tend to overfit the data, especially if poorly trained (small dataset), such a model which solves complex problem need a whole lot of data, and getting vast amounts of labeled data for supervised models can be really difficult, considering the time and effort it takes to label data.

		-> Thus, the key motivation, to use, transfer learning in order to make better results 

- Classification Using INCEPTION pretrained model :




||Bare Model| |Adding Dropout Layer||Setting Adaptative learning rate||
:------------:|:------:|:---------:|:------:|:---------:|:------:|:---------:
|	  |  Train  | Test |  Train  | Test |  Train  | Test
loss |    0.0909 | 0.6521| 0.0989 |   0.4210|0.0219|0.3277  
accuracy | 0.9710   |0.9107  |0.9750 | 0.9214|0.9923 |0.9427

			-> As expected the dropout helped with the overfitting, we decreased the val_loss from 0.6 to 0.4  also the accuracy increased from 91% to 92.2%.
			
			-> Another clue about reducing the overfitting is that the rate on which the training loss decrease compared to the rate of the validation loss decrease is much slower, which mean we don't overfit very fast, thus we give time for the model to learn and generalize more. 

			-> Using more suitable learning rate keeps us on from diverging to a sub optimal set of weights. and thus increase the performance of our model.

