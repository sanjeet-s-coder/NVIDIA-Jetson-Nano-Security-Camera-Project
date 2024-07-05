# Nvidia Jetson Nano Security Camera

 
This is a Object Detection Security camera I made using NVIDIA's Jetson Nano. An AI-powered security camera typically uses a convolutional neural network (CNN) for image recognition and object detection. This network processes video feeds in real-time, analyzing frames to detect motion, recognize faces, or identify unusual activities by learning patterns and features from vast datasets during training. Creating an AI-powered security camera using NVIDIA's Jetson Nano can significantly enhance security in residential, commercial, and public spaces by providing real-time monitoring and alerts, potentially reducing crime rates. However, it also raises privacy concerns due to increased surveillance and data collection.


![add image descrition here](direct image link here)

# The Algorithm

from jetson_inference import detectNet
from jetson_utils import videoSource, videoOutput

Initialize the neural network for object detection using SSD-Mobilenet-v2 with a confidence threshold of 0.5
net = detectNet("ssd-mobilenet-v2", threshold=0.5)

Initialize the camera input using videoSource, assuming the camera is connected to /dev/video0
camera = videoSource("/dev/video0")

Initialize the display output using videoOutput to show the processed video stream
display = videoOutput("display://0")

Continuously process frames from the camera and display the results until the display stops streaming
while display.IsStreaming():
    Capture a frame from the camera
    img = camera.Capture()

    # If the captured image is None, skip the current iteration of the loop
    if img is None:
        continue

    # Perform object detection on the captured image using the neural network
    detections = net.Detect(img)
    
    # Render the annotated image with bounding boxes and labels on the display
    display.Render(img)
    
    # Set the status text displayed on the output indicating the current FPS of the neural network
    display.SetStatus("Object Detection | Network {:.0f} FPS".format(net.GetNetworkFPS())) 

## Running this project

1. Open up a new terminal on the Jetson Nano and type this command
   python3 my-detection1.py
   **Make sure the Nano is connnected to a monitor with a display or else you will get a error**
3. Install the groundtruth library in the Security Camera Folder

[View a video explanation here](video link)
