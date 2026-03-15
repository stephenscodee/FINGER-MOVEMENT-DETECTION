# Finger Movement Detection

This project provides a real-time hand and finger movement tracking script using Python, OpenCV, and Google's MediaPipe framework. It captures video from your webcam and dynamically identifies all 21 3D hand landmarks, drawing distinct markers over the joints and fingertips of up to two hands simultaneously.

## Features
- **Real-Time Tracking**: Processes webcam video feed smoothly using the efficient MediaPipe Hand Landmarker model.
- **Full Hand Mapping**: Draws indicators on all 21 key points (landmarks) of each detected hand, not just a single finger.
- **Multi-Hand Support**: Configured to track up to two hands at the same time.

## Prerequisites
Before running the script, ensure you have Python 3 installed along with the required dependencies.

Install the necessary libraries using `pip`:
```bash
pip install opencv-python mediapipe
```

You will also need the MediaPipe AI task model file (`hand_landmarker.task`) in the same directory as the script. You can download it directly from Google here:
```bash
curl -o hand_landmarker.task "https://storage.googleapis.com/mediapipe-models/hand_landmarker/hand_landmarker/float16/1/hand_landmarker.task"
```

## How It Works (Code Overview)
- **Initialization**: The script uses `mediapipe.tasks.python.vision.HandLandmarker` options to configure the model in video stream mode, setting the detection and tracking confidences to 0.9 (90%) for high accuracy.
- **Video Capture**: It opens the default webcam (ID `0`) via OpenCV (`cv2.VideoCapture`).
- **Processing Loop**: For every frame, the script:
  - Flips the image horizontally for a mirror-like experience.
  - Converts the BGR colorspace (used by OpenCV) to RGB (required by MediaPipe).
  - Passes the image data to the `detector.detect()` method.
- **Rendering**: If hands are found in the frame, it iterates through `result.hand_landmarks`. For every individual `landmark` across the 21 points of the hand, it calculates its standard (x, y) coordinates relative to the screen dimensions and draws a purple circle using `cv2.circle()`.
- **Exit Condition**: The loop breaks and the program closes gracefully when the `q` key is pressed on the keyboard.

## Usage
To start the tracker, run the Python script from your terminal:
```bash
python3 FINGER_MOVEMENT.PY
```
*Note for macOS users: Ensure that your Terminal (or the IDE you are running the code from) has been granted Camera permissions under System Settings > Privacy & Security > Camera.*
