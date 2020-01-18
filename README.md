# Sign language recognition with RNN and Mediapipe 
## with multi hand tracking
Sign language gesture recognition using a reccurent neural network(RNN) with Mediapipe hand tracking. 

This project is for academic purpose. Thank you for Google's Mediapipe team :)

## Data Preprocessing with hand tracking(Desktop)
Create training data on Desktop with input video using [Hand Tracking](https://github.com/google/mediapipe/blob/master/mediapipe/docs/hand_tracking_mobile_gpu.md).
Gesture recognition with deep learning model can be done with only **42 hand landmarks** RNN training per frame.

**CUSTOMIZE:**
- Use video input instead of Webcam on Desktop to train with video data
- Extract hand landmarks for every frame per one word and make it into one txt file

### 1. Set up Hand Tracking framework
* Install Medapipe
```shell
  git clone https://github.com/google/mediapipe.git
```
See the rest of installation documents [here](https://mediapipe.readthedocs.io/en/latest/install.html).
* Change **/end_loop_calculator.h** file
```shell
  cd ~/mediapipe/mediapipe/calculators/core
  rm end_loop_calculator.h
```
to our new /end_loop_calculator.h file in the modified_mediapipe folder.

* Change **demo_run_graph_main.cc** file 
```shell
  cd ~/mediapipe/mediapipe/examples/desktop
  rm demo_run_graph_main.cc
```
to our new demo_run_graph_main.cc file in the modified_mediapipe folder.

* Change **landmarks_to_render_data_calculator.cc** file
```shell
  cd ~/mediapipe/mediapipe/calculators/util
  rm landmarks_to_render_data_calculator.cc
```
to our new landmarks_to_render_data_calculator.cc file in the modified_mediapipe folder.

### 2. Create you own training data
Make **train_videos** and **test_videos** for each sign language word in one folder. Copy **build.by** file in util folder to your mediapipe directory. (Currently there may be a TabError. You may need to change the tab manually.)
* Usage

To make mp4 file and txt file with mediapipe automatically, run
```shell
  python build.py --input_data_path=[INPUT_PATH] --output_data_path=[OUTPUT_PATH]
```
inside mediapipe directory. (example: python build.py --input_data_path=/Users/anna/SLR/input_video/ --output_data_path=/Users/anna/SLR/output_video/)

Change INPUT_PATH, OUTPUT_PATH to your own folder directory path. INPUT_PATH is path to your input videos. OUTPUT_PATH is where all the hand-tracked mp4 files and txt files of 42 landmarks will be saved.

For example:
```shell
input_videos
├── Apple
│   ├── IMG_2733.MOV
│   ├── IMG_2734.MOV
│   ├── IMG_2735.MOV
│   └── IMG_2736.MOV
├── Bird
│   ├── IMG_2631.MOV
│   ├── IMG_2632.MOV
│   ├── IMG_2633.MOV
│   └── IMG_2634.MOV
└── Sorry
    ├── IMG_2472.MOV
    ├── IMG_2473.MOV
    ├── IMG_2474.MOV
    └── IMG_2475.MOV
    ...
```
OUTPUT_PATH is initially empty directory and when build is done, Mp4 and txt files will be extracted to your own folder path. 

Created folder example:
```shell
output_data
├── _Apple
│   ├── IMG_2733.mp4
│   ├── IMG_2734.mp4
│   ├── IMG_2735.mp4
│   └── IMG_2736.mp4
└── Bird
    ├── IMG_2472.txt
    ├── IMG_2473.txt
    ├── IMG_2474.txt
    └── IMG_2475.txt
    ...
```
(DO NOT use space bar or '_' to your folder path and video name ex) Apple_pie (X))

Our ASL word example:

| word | word | word | word |
|:------:|:------:|:------:|:------:|
|Apple|Bird|Blue|Cents|
|Child|Cow|Drink|Green|
|Hello|Like|Metoo|No|
|Orange|Sorry|Thankyou|Where|
|Who|Yes|You|   |






### 3. Train RNN model

* Train
```shell
  python LSTM.py --input_file=[PKL_FILE]
```
Add path to preprocessed pkl file into PKL_FILE.

Watch [this video](https://www.youtube.com/watch?v=5epWNiv5EKk&t=77s) for the overall workflow.
[more details](https://www.slideshare.net/JiHyunKim204)




