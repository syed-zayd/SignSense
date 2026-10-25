# SignSense

**SignSense** is a real-time American Sign Language (ASL) letter recognition system developed as part of the SE101 course at the University of Waterloo. The system uses a Raspberry Pi Zero W and a camera module to capture hand orientation landmarks, enabling the prediction of ASL letters in real-time using a trained ML model. This repository is a fork and only contains the main branch with programs for both the Pi and the server running the model.

## Installation

### Requirements

Before running the project, make sure you have the following:

- **Raspberry Pi Zero W** with a camera module and audio output
- Python 3.10.x
- TensorFlow
- Flask
- OpenCV
- NumPy
- MediaPipe
- LanguageTool

### Setup

1. **On the Raspberry Pi**:
   - Clone the repository and install the camera, speech and server libraries:
     ```bash
     sudo apt install python3-picamera2 espeak
     pip install flask opencv-python
     ```
   - Start the Flask server on the Raspberry Pi by running:
     ```bash
     python flaskie.py
     ```

2. **On an external computer** (same network as the Raspberry Pi):
   - Clone the repository and install the required libraries:
     ```bash
     pip install -r requirements.txt
     ```
   - LanguageTool needs Java installed.
   - Point the scripts at the Pi if it is not reachable as `raspberrypi.local`:
     ```bash
     export SIGNSENSE_PI_URL=http://<pi-address>:8888
     ```
   - Run the `test.py` script to start receiving and displaying the ASL predictions:
     ```bash
     python test.py
     ```

### Retraining the model

`dataset_preparation.py` turns the images in `asl_alphabet_dataset/` into hand landmarks in
`dataset.pickle`, and `training_model.py` trains on that file and saves
`SignLanguageNeuralNetwork.h5`.

## Usage

1. Once `flaskie.py` is running on the Raspberry Pi, and `test.py` is running on the external computer, the camera module on the Raspberry Pi will begin capturing signs.
2. The system will stream the captured video to the external computer, predict the ASL letter, and send the result back to the Raspberry Pi for text-to-speech output.
