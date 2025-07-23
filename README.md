
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

**tracking scripts**

*tkinterdash.py* - a file that opens a tkinter dashboard containing a 1) regional counter, 2) density calculator, 3) general counter, 4) raw video, and 5) an estimated density of that hour or so (give or take).  Outputs densities to a file. 

*tkinterhunger.py* - a file that opens a tkinter dashboard containing a tracker for the video feed, surrounded with corresponding graphs for speeds, energy, etc. API code links to pushover, which is to be changed to your own API - this will ping a notification for unnatural directions/speeds, and also inform if there has been lots of movement after feeding (possible signs of hunger), and additionally ping if there has been a immobile fish for a long while.

*tkinterfeed.py*
Pseudocode: 
opens the camera, runs tracking like all others - instead, once fed; runs multiple detection models - the tracking + feed detection, and in the time that passes, tracks how many have disappeared --> thus determining hunger levels ; furthermore, either through the model or through an opencv button, will track for about 15 minutes and see the average speeds/energy consumption - if not a lot, can safely determine they do not want to move "to" the food, and thus aren't hungry.
Any other methods?
* track time after feeding, and track irregular movement?

**data analysis scripts**

*lstm.py* - file that trains the predictive lstm model. Modifications can be made if needed 

*dashboard.py* - tkinter dashboard, which displays all the values of importance in a neat graphical interface. Updates if the files is updated

*scrapehuceen.py* - a webscraping script made with selenium to locate and extract data from the huceen PLC dashboard quickly and conveniently. Extracts every 10 minutes, although this can be changed, as well as the mouse positions(due to the lack of selectable css and html objects on the webpage) depending on the screen size.

*analysisboard.py* - tkinter dashboard that periodically updates the information every time the scraping file updates the data, and updates its predictions as well. The board provides the current values, a historical view of the last hour, and a prediction for the next hour, although the time predicted can be changed to up to the next 1.5 hours.

**training scripts**

*train.py* - normal YOLO training script that allows any dataset to be exported in YOLO format then trained. Run this file with the PATH changed to the path to the data.yaml in your dataset to train a model.

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

## Step by step guide to setting up:

1. Clone the repository:
   ```bash
   git clone https://github.com/popperda/fish-tracker.git
   cd fish-tracker
   ```
2. Install dependencies using `requirements.txt`:
   ```bash
   pip install -r requirements.txt
   ```
3. Train your datasets using Path A or Path B as specified above. Once the dataset is finished in roboflow, export it as a YOLO 11 dataset. Put the dataset folder somewhere accessible in the fish-tracker directory.
4. Change PATH in the *train.py* file to the dataset's data.yaml. It is recommended to edit this in vscode or some other editor. Then tweak the model parameters, and run *train.py*. The model location should be displayed in the terminal. 
    ```bash
   python train.py
   ```

5. In the scripts folder, now replace the model.pt with the path to your model.

6. Then run any script as needed! EG:
    ```bash
   python tkinterhunger.py #fish tracking and inactivity estimation
   ```

PLC management

1. navigate to the scraping folder
    ```bash
   cd sensors
   ```

2. in *scrape.py*, test it and see if the button clicks are accurate. If not, do some trial and error to get it right.
    ```bash
   python scrape.py
   ```
    After running, make some changes and edits depending on where the mouse is clicking. See this video: ___
3. Then, once confirmed, run *automatescrape.py*. This will collect data every 10 minutes or so.
    ```bash
   python automatescrape.py
   ```

4. Afterwards, run the analysisboard.py - this will provide a dashboard for the data, as well as make predictions.
    ```bash
   python analysisboard.py
   ```


Video on the whole process:
