# hand-gesture-remote-controller
The main repository only contains these gestures.
![valid gestures](https://raw.github.com/AladdinT/hand-gesture-remote-controller/main/media/remote_gestures.png "remote_gestures")
<br>
Estimates hand pose using MediaPipe.<br> 
This is a sample program that recognizes hand gestures with a simple MLP using the detected key points.
<br> 
_️**This is forked from [kinivi/hand-gesture-recognition-mediapipe](https://github.com/kinivi/hand-gesture-recognition-mediapipe) and [AladdinT/hand-gesture-remote-controller](https://github.com/AladdinT/hand-gesture-remote-controller/tree/main).**_
<br>
The main aim is to replace a remote controller with some hand gestures. As this model is intended to be used in a smart mirror application as a navigator.

<br>
<img src="https://raw.github.com/AladdinT/hand-gesture-remote-controller/main/media/animation.gif" width="400" height="300">
<br>


We add new gesture for <b>zoom mode</b> more over we add another part which pass the key points' history into point history model to predict whether the action is zoom in or zoom out.
<br>


![zoom](https://github.com/farhad-99/hand-gesture-movement-recognition/assets/96428374/b2695f5a-7b41-4f6d-bc3f-cd8071ef4bde)





https://github.com/farhad-99/hand-gesture-movement-recognition/assets/96428374/6f0dc66c-f8ab-48af-b6ae-374c8a8949da



<br>
The
# Demo
Here's how to run the demo using your webcam.
```bash
python app.py
```

The following options can be specified when running the demo.
* --device<br>Specifying the camera device number (Default：0)
* --width<br>Width at the time of camera capture (Default：960)
* --height<br>Height at the time of camera capture (Default：540)
* --use_static_image_mode<br>Whether to use static_image_mode option for MediaPipe inference (Default：Unspecified)
* --min_detection_confidence<br>
Detection confidence threshold (Default：0.6)
* --min_tracking_confidence<br>
Tracking confidence threshold (Default：0.5)

# Directory
<pre>
│  app.py
│  keypoint_classification.ipynb
│  point_history_classification.ipynb
│  
├─model
│  └─keypoint_classifier
│     │  keypoint.csv
│     │  keypoint_classifier.hdf5
│     │  keypoint_classifier.py
│     │  keypoint_classifier.tflite
│     └─ keypoint_classifier_label.csv
│
└─utils
    └─cvfpscalc.py
</pre>
### app.py
This is a sample program for real-time inference.<br>
You can also collect training data (key points) for hand sign recognition.<br>

#### Collecting data for new gesture
You should run app.py and press 'k' to enter the recording key_point mode. When you see 'MODE: Logging key point,' you can make your desired hand pose and press a number (this number will be the class number of your hand gesture in the training stage). The number of collected data should be in the same order as other classes to avoid biases in our model

#### Collecting data for new movement
You should run app.py and press 'h' to enter the recording key_point mode. When you see 'MODE: Logging Point History,' you can make your desired movement and press a number (this number will be the class number of your hand movement in the training stage). The amount of collected data should be in the same order as other classes to avoid biases in our model.
you can edit key points' detail here

https://github.com/farhad-99/hand-gesture-movement-recognition/blob/b0075fe728eb6c8d29247dd099dc5f81469a93d2/app.py#L145

here is the keypoint numbers map:
![hand landmark](https://github.com/farhad-99/hand-gesture-movement-recognition/assets/96428374/0fad6aea-203b-4cf3-b78b-08ec2afd5fa3)


For using the history_point_model, we should define a start gesture. When the gesture is recognized, our algorithm proceeds to the next step, and then the history_point_model begins to infer. So, for each movement, we can deploy a specific model.




### model_training.ipynb
This is a model training script for hand sign recognition.<br>
please refer to [main repo](https://github.com/kinivi/hand-gesture-recognition-mediapipe) for better understanding of how the data collection and training process works. 
<br>
![confusion matrix](https://raw.github.com/AladdinT/hand-gesture-remote-controller/main/media/confusion_matrix.png "confusion_matrix")


### model/keypoint_classifier
This directory stores files related to hand sign recognition.<br>
The following files are stored.
* Training data(keypoint.csv)
* Trained model(keypoint_classifier.tflite)
* Label data(keypoint_classifier_label.csv)
* Inference module(keypoint_classifier.py)

### utils/cvfpscalc.py
This is a module for FPS measurement.
