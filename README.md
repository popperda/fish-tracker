
# Fish Analysis Module

Helps you set up a personal fish tracker with some preset dashboards and functions available. By Jared!


## Introduction

This github repo is made for any fish hobbyist or budding aquaculturist who is looking into implementing an AI model within their own tanks through the use of camera(s). This READme will contain steps to setting up a model that can be used to **track fish**, **check their speeds**, **change in direction**, **check regional feeding patterns** and even **estimate lengths** which could be used to make a rough estimate of their size and even weight using *YOLOv11*. 


## Demo

A basic demo of each functionality:

Tracking:

![demo](https://github.com/user-attachments/assets/1b1ddf7a-f8cf-4c49-95e0-76c562ee8716)

Hunger tracker (Energy tracking, dead fish, fish movement irregularity ALL IN ONE)

![demo](https://github.com/user-attachments/assets/6dea6af9-1f0e-46b7-a396-0105edcac964)

Density estimation

![dash](https://github.com/user-attachments/assets/5273304a-fc8c-458f-a116-9d19c0aef702)




## Scripts

This is a brief description of what each script in the scripts folder does and what can be expected.
## Deployment

To deploy your own version there are multiple paths to take:

**Path A** - develop your own dataset (RECOMMENDED)

From personal testing and development of models, although there are a plethora of underwater/fish datasets online from roboflow or elsewhere, the best and most customized models will be from your own images, and won't require too many images. 

To make and label your own dataset, follow the steps in this following guide:
https://blog.roboflow.com/yolov11-how-to-train-custom-data/

Or alternatively use this guide: 
https://colab.research.google.com/github/EdjeElectronics/Train-and-Deploy-YOLO-Models/blob/main/Train_YOLO_Models.ipynb

Once the datasets are created and labelled, the hard part is over. 



**Path B** - use online datasets 

Roboflow is a good source for this repo as we will be using its ability to convert the dataset into YOLO formatting. However, any dataset can be converted to YOLO if need be. 
Some good examples: 

- https://universe.roboflow.com/razvan-jk1bz/fish-detection-kvnwj/dataset/3
- https://alzayats.github.io/DeepFish/


**Traning** - train the model and set it up

Training models on datasets in YOLO is relatively simple, and some example training scripts are in the training folder in the repo. However, feel free to make changes and tweak the model for any changes using YOLO11's documentation for training here https://docs.ultralytics.com/modes/train/#augmentation-settings-and-hyperparameters.

Once a model has been trained, it will tell you in the terminal where the models are being stored. Take the best.pt, then rename it. Choose from one of the scripts in the script folder in this github repository, then download it and create an environment where the model is in the same folder as the script. Once that is done, go to the script and replace *[rename]* with your model's name. Once that is done, make sure that all dependencies in the imports are installed and run the script by its own. Then, all you need is to run the python script and ensure a camera is connected to your device.

**Script Setup** - get the scripts working

Either download individual files from the repo or clone the repo; then auto-install the required packages at the requirements.txt.
Once the packages have been installed, the next step is to open and run the files. A description of the file is included at the top of each file. Once connected to a camera, the files should be able to work properly. Some files depend on preset values (eg. how fast a fish has to be to be speeding, or the pixel-cm ratio) which may have to change based on any new setups.

