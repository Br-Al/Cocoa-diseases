# Cocoa-diseasis
Using OpenVino and OAK-D combined, we will train an object detection model(PyTorch) to identify all types of insect pests for cocoa trees, to identify the symptoms and signs present on each part of the cocoa tree (leaves, pods, stems, etc.).
## Problem
30 to 40% of the world's annual cocoa production is lost due to insects and pathologies. This represents around 558,000 tones out of a total of over 3.9 million annual production. Cocoa is produced mainly by developing countries, which do not have the appropriate technology to ensure its healthy and sustainable production. How to use artificial intelligence to detect insects and pathologies harmful to cocoa production?
## Phase 1
The first phase consists to build a detector model to detect the two main cocoa pathologies present in Africa (black pod root and pod borer). Then deploy the model into OAK-D device.
## Solution
### Framework and Pre-trained model
We choose Pytorch as framework because of the flexibility. It is easy to customize pre-trained models and train on custom datasets. Our goal is to detect disease symptoms on cocoa pod. To do that we will perform instance segmentation with mask on images. The best model to perform this task is the Mask RCNN model from Torchvision. We will re-train this model on ours datasets.
### Data collection and annotation
The first step of this phase consist of data preparation. To train our model, we need a set of images of cocoa pod.
#### Data collection
We have collected data from Google image and from Kaggle cocoa diseases dataset. Our dataset has the following characteristics:
* A sample for each category : 3344 images of healthy cocoa pod, 943 images of cocoa pod with black pod rot, 103 images of cocoa pod with pod borer
* Total of 4390 images
* Image size 3*1080*1080

![image](https://user-images.githubusercontent.com/58564800/134661654-b89cbdae-83ed-4a19-b9af-18e162643690.png)
#### Data annotation
For data annotation, we used SuperAnnotation tool and polygon annotation technic.
![image](https://user-images.githubusercontent.com/58564800/134661820-6cd257b1-51f0-41c1-933a-a0f0bf768b63.png)
![image](https://user-images.githubusercontent.com/58564800/134661940-ccb9e4f9-1573-42b0-9a9e-fa49ba6b036f.png)
![image](https://user-images.githubusercontent.com/58564800/134661960-53f66e39-ced2-4291-8cb2-b6709647e391.png)
![image](https://user-images.githubusercontent.com/58564800/134661982-9969ee90-25b3-4826-89d9-b196a6dfe688.png)
![image](https://user-images.githubusercontent.com/58564800/134662049-ec9e1cb0-6577-4013-9053-1d5e436ea742.png)
At the end of this step we have a dataset of 2435 annotated images. We also split the dataset as:
*	80% for training (1930 images)
*	20% for validation (506 images)
We exported our dataset in COCO format.
### Train the model on our dataset
You will find the notebook containing the code for loading the data, training loop, validation and test by following this [link ](https://colab.research.google.com/drive/18Rv7weWmpvTNdWWIFqEMyt5WbB6fRQ3h?usp=sharing "Notebook")
#### Metrics (Bounding Boxes & segmentations)
![image](https://user-images.githubusercontent.com/58564800/134663077-cb5deb7f-01ef-487c-973a-66232f8a9881.png)
![image](https://user-images.githubusercontent.com/58564800/134663101-14beae01-a041-4d99-b4c9-5b6714bf9a80.png)
![image](https://user-images.githubusercontent.com/58564800/134663109-94c0f8f1-13a0-4225-82f7-45fa54d45e45.png)
![image](https://user-images.githubusercontent.com/58564800/134663134-1ea97165-b583-4cef-9459-5374aec0cd53.png)
![image](https://user-images.githubusercontent.com/58564800/134663147-c9de1752-d88d-40a1-bb66-9430e212864a.png)
![image](https://user-images.githubusercontent.com/58564800/134663165-75504c73-67da-4ff1-971e-5f028a4b952f.png)
11.	References

Pytorch documentation & tutorial: [(https://pytorch.org/tutorials/intermediate/torchvision_tutorial.html)]
Depthai Documentation : [(https://docs.luxonis.com/en/latest/#depthai-s-documentation)]
Kaggle dataset: [(https://www.kaggle.com/zaldyjr/cacao-diseases)]
Tensorflow images segmentation tutorial : [(https://www.tensorflow.org/tutorials/images/segmentation)]
Learn OpenCV tutorials : [(https://learnopencv.com/mask-r-cnn-instance-segmentation-with-pytorch/)]
Udacity course : [(https://www.udacity.com/course/intel-edge-ai-for-iot-developers-nanodegree--nd131)]
