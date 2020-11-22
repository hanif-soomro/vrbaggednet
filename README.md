<h2 align="left">VRBagged-Net</h2>
The script implements VRBagged-Net classification framework for flood classification. It is a binary classification framework, which utilizes deep learning models Visual Geometry Group (VGG) and Residual Network (ResNet), along with the technique of Bootstrap aggregating (Bagging). Detailed steps for implementation are given below:

<h3 align="left">1. Data Augmentation</h3>

Data augmentation technique is applied with the help of Augmentor library, which can be installed using: 
```sh
!pip install Augmentor
```

<h3 align="left"> 2. Training </h3>
The images of train-set are stored in the directories of their respective class i-e "Flood related topic" aand "No-flood related topic". 

* dir_train/
	* dir_flood/ </br>
		*  01_flood.jpg </br>
		*  02_flood.jpg </br>
		*  03_flood.jpg </br>
	* dir_noflood/ </br>
		*  01_noflood.jpg </br>
		*  02_noflood.jpg </br>
		*  03_noflood.jpg </br>


Stratified and equal-sized random samples are selected from each of the class for the training of model. 
<h4 align="left">Pretrained Convolutional Neural Networks </h4> 
The pretrained VGG16-Hybrid can be downloaded from following link: 
[VGG16-Hybrid1365](https://github.com/GKalliatakis/Keras-VGG16-places365) 

The weights of VGG16-hybrid1365 can be loaded by: 

```sh
VGG16_Hybrid_1365(weights='places', include_top=True)
```


It the weights of ResNet50, pretrained on ImageNet can be loaded by: 
```sh
ResNet50(weights='imagenet',include_top=True,input_shape=(224, 224, 3))
```
<h3 align="left">3. Prediction on Test Data </h3>
Two models are trained during train-stage (i-e VGG16 and ResNet50). These both models are separately used for the prediction of each image in test-set. The prediction of each model is collected in form of confidence and averaged: 
<h4 align="left">Majority Voting </h4>
This process is repeated for multiple times and discrete prediction (either 0 or 1) is stored in csv file for each time. Finally, majority voting is applied to generate final outcome of VRBagged-Net. 
