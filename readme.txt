
# Car Parking Space Detection Project

## Overview

This project provides an implementation for detecting available parking spaces in a parking lot using OpenCV, cvzone, and other Python libraries. The program reads video footage of a parking lot and determines which parking spaces are free or occupied by analyzing the pixel intensity in predefined parking areas. It also includes a graphical interface to manually select and edit parking space positions.

## Table of Contents
- [Technologies Used](#technologies-used)
- [Features](#features)
- [Project Files](#project-files)
- [Setup Instructions](#setup-instructions)
- [How the Code Works](#how-the-code-works)
  - [Parking Space Detection](#parking-space-detection)
  - [Selecting Parking Positions](#selecting-parking-positions)
- [How to Use the Project](#how-to-use-the-project)
- [Future Improvements](#future-improvements)

## Technologies Used
- Python 3.x
- OpenCV
- Numpy
- cvzone
- Pickle

## Features
- Automatic detection of available parking spaces in video footage.
- Adjustable parameters using trackbars for fine-tuning detection accuracy.
- Graphical interface for manually adding and removing parking space positions.
- Displays the number of free parking spots dynamically.
  
## Project Files
1. `carPark.mp4` - The video footage of the parking lot.
2. `carParkImg.png` - A static image used for selecting parking spots.
3. `CarParkPos` - A binary file to store the coordinates of parking spots.
4. `parking_space_detection.py` - The main Python script for parking space detection.
5. `position_selector.py` - A helper Python script for selecting and saving parking space positions.

## Setup Instructions

### Prerequisites:
- Python 3.x installed on your system.
- Required Python libraries:
  - OpenCV (`cv2`)
  - Numpy
  - cvzone
  - Pickle

### Installation:
1. Clone the repository to your local machine.
2. Install the required libraries using pip:
    ```bash
    pip install opencv-python opencv-python-headless numpy cvzone
    ```
3. Place the video file (`carPark.mp4`) and image (`carParkImg.png`) in the project directory.

### Running the Project:
1. To manually select parking space positions:
    ```bash
    python position_selector.py
    ```
2. To run the parking space detection script:
    ```bash
    python parking_space_detection.py
    ```

## How the Code Works

### Parking Space Detection
1. **Loading Parking Positions**: 
    - Predefined parking space positions are loaded from the `CarParkPos` file using the `pickle` library. These positions define areas in the parking lot that are analyzed to detect whether a car is parked in them.

2. **Video Processing**:
    - The video footage (`carPark.mp4`) is read frame by frame.
    - The frames are converted to grayscale and blurred using Gaussian blur to reduce noise.
    - Adaptive thresholding is applied to create a binary image where parking spaces can be more easily detected.
    - The binary image is further processed with median blur and dilation to fill small gaps in the detected regions.

3. **Detecting Occupied Spaces**:
    - For each parking position, the program crops out the corresponding region from the thresholded image.
    - It calculates the number of non-zero pixels in this region to determine whether the space is occupied. A threshold (e.g., 900 pixels) is used to decide if a space is empty or occupied.
    - Occupied spaces are marked with red rectangles, while free spaces are marked with green rectangles.

4. **Display**:
    - The current number of free spaces is displayed on the video.
    - Press `q` to exit the video.

### Selecting Parking Positions
- A separate script (`position_selector.py`) allows users to manually select parking spaces on a static image (`carParkImg.png`).
- Users can left-click to add a new parking position and right-click to remove an existing one.
- The coordinates of the selected parking spaces are saved to the `CarParkPos` file using the `pickle` library.

## How to Use the Project
1. **Adding Parking Positions**:
    - Run `position_selector.py` to open an image of the parking lot.
    - Click on the image to add parking spots or remove them by right-clicking on existing rectangles.
    - The selected positions will be saved automatically.

2. **Detecting Parking Spaces**:
    - Run `parking_space_detection.py` to analyze a video of the parking lot.
    - The program will automatically detect which spots are occupied and display this information on the video feed.
    - You can adjust the detection sensitivity by using the trackbars for threshold values (`Val1`, `Val2`, and `Val3`).

## Future Improvements
- Implementing object tracking to follow cars into and out of the parking lot for more accurate detection.
- Using deep learning models (e.g., YOLO, SSD) to detect cars and improve accuracy in complex scenarios.
- Integrating a web-based or mobile interface for real-time monitoring of parking spaces.
- Adding a feature to notify users when a certain number of spaces become available.

## Credits
- OpenCV for video processing and image manipulation.
- cvzone for convenient utility functions and text rendering.
