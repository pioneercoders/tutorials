# Computer Vision

Computer Vision enables systems to understand images and videos.

## Why Computer Vision Matters

Computer vision powers medical imaging, retail analytics, autonomous vehicles, surveillance, and visual search.

## Image Classification

Image classification predicts what object is present in an image.

### Example

```python
from tensorflow import keras

model = keras.models.load_model('image_classifier.h5')
pred = model.predict(image_batch)
```

## Object Detection

Object detection identifies multiple objects and their locations in an image.

### Typical outputs
- Bounding boxes
- Class labels
- Confidence scores

## YOLO

YOLO is a fast real-time object detection model family.

### Why teams use YOLO
- Very fast inference
- Good for live video
- Easier to deploy on edge devices

## OpenCV

OpenCV is a popular library for image preprocessing and computer vision pipelines.

### Example

```python
import cv2

img = cv2.imread('image.jpg')
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
faces = cv2.CascadeClassifier('haarcascade_frontalface_default.xml').detectMultiScale(gray)
```

## Face Recognition

Face recognition systems identify or verify a person from an image.

### Common steps
1. Detect face
2. Align face
3. Extract embedding
4. Compare embeddings

## Image Segmentation

Image segmentation classifies each pixel, not just each image.

### Use cases
- Medical imaging
- Autonomous driving
- Background removal

## OCR

OCR extracts text from images.

### Example workflow
1. Preprocess image
2. Detect text regions
3. Apply recognition model
4. Post-process output

## Pose Detection

Pose detection estimates the position and orientation of joints in the body.

### Applications
- Fitness tracking
- Gesture recognition
- Sports analytics

## Vision Pipeline

```python
import cv2
import numpy as np

img = cv2.imread('sample.jpg')
img = cv2.resize(img, (224, 224))
img = img.astype('float32') / 255.0

# model predicts class
prediction = model.predict(np.expand_dims(img, axis=0))
```

## Challenges in Computer Vision

- Lighting changes
- Occlusion
- Scale variation
- Domain shift

## Practical Interview Questions

- How is object detection different from image classification?
- Why are CNNs effective for images?
- What is the difference between segmentation and detection?

## Summary

Computer vision turns images into structured insights. It is foundational for healthcare, retail, safety, robotics, and automation.
