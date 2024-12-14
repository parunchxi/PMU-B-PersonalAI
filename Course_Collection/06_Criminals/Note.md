# AI for arresting criminals

The Research and Development of Tracking Systems for Arresting Criminals Using Artificial Intelligence project enhances police efficiency and public safety by using AI-powered systems for crime monitoring, evidence recording via CCTV, and real-time detection and tracking of suspects or vehicles.

## Real-Time Object Detection

### Object Detection Overview

- **Definition:** Object detection involves both locating and classifying objects within an image or video.
- **Goal:** Develop algorithms capable of performing object detection quickly and with high accuracy.

### Importance of Object Detection

- **Power of Visual Modality:** Humans can detect objects and interpret visual information in real-time using only their vision, without requiring specialized sensors like radar.
- **Applications in Robotics:** For responsive robotic systems, vision-based object detection in near real-time is critical. This eliminates the need for complex or specialized sensors.

## YOLO Overview

- **Grid Division:** An input image is divided into an **S × S grid**.
- **Bounding Box Prediction:** Each grid cell predicts **B bounding boxes**.
- **Predictions for Each Box:**
  - **x, y:** Center coordinates of the object relative to the grid cell.
  - **w, h:** Width and height of the bounding box.
  - **Confidence:** Probability that the bounding box contains an object.

## YOLO Training

- **Regression Approach:** YOLO treats object detection as a regression problem.
- **Input (X):** An image represented as a matrix of dimensions: **width × height × RGB values**.
- **Output (Y):** A tensor of size **S × S × (B × 5 + C)**, where:
  - **B × 5:** Represents the bounding box parameters (x, y, w, h, confidence).
  - **C:** Represents the class probability distribution for each grid cell.

## YOLO Architecture

- **Input Dimensions:** 448 × 448 × 3 (image with RGB channels).
- **Network:** 7 convolutional layers for feature extraction.
- **Parameters:**
  - **S = 7**: Grid size.
  - **B = 2**: Number of bounding boxes per grid cell.
  - **C = 20**: Number of object classes.
- **Output Tensor:** S × S × (5B + C) = 7 × 7 × 30.

## Non-Maximal Suppression (NMS)

- **Purpose:** Finalize predictions by eliminating redundant bounding boxes.
- **Steps:**
  1. Filter bounding boxes with low confidence scores.
  2. Compute the class score using the formula: **Pr(Class | Object)**.
  3. Retain the bounding box with the highest confidence and discard others with significant overlap.

## YOLO Predictions

- **Handling Overlaps:** YOLO ensures the bounding box with the **highest confidence** is retained.
- **Improvement:** This post-processing step adds 2–3% to the final **mean Average Precision (mAP)** score.

## YOLO Objective Function

1. **Localization Loss:**
   - Measures how accurately the bounding box matches the ground truth.
   - Includes position (x, y) error and size (w, h) error.
   - Uses Mean Squared Error (MSE) for calculations.
2. **Confidence Loss:**
   - Penalizes incorrect predictions for bounding box confidence.
3. **Classification Loss:**
   - Evaluates the accuracy of class predictions for objects.

## YOLOv8

- **Backbone:** Similar to YOLOv5 but incorporates the **C2f module** (Cross-Stage Partial Bottleneck with two convolutions).
- **C2f Module:** Combines high-level features and contextual information to improve detection accuracy.
- **Performance:** Trained on datasets like COCO, delivering superior detection efficiency.

## Conclusion

This research highlights the application of AI for enhancing police efficiency in Thailand by:

- Leveraging object detection to analyze crime data.
- Utilizing intelligent CCTV for real-time crime monitoring.
- Integrating real-time alerts for suspicious activities to support law enforcement.
