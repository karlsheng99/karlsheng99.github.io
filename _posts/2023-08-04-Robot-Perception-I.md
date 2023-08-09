---
layout: post
title: "Robot Perception I"
description: "Robot Perception I"
date: 2023-08-04
feature_image: 
tags: [ROS, OpenCV, Raspberry Pi, Linux]
---

A study note for Computer Vision in ROS with OpenCV.

<!--more-->

# Robot Perception I

### Bridging Images between OpenCV and ROS

![Untitled](/images/2023-08-04/Untitled.png)

### Thresholding

Simple Thresholding

```python
cv.threshold(	src, thresh, maxval, type	)
```

![Untitled](/images/2023-08-04/Untitled%201.png)

![Untitled](/images/2023-08-04/Untitled%202.png)

Adaptive thresholding

- calculates the threshold for a small region of the image
- different thresholds will be calculated for different regions of the same image
- better robustness to varying illumination

```python
cv.adaptiveThreshold(	src, maxValue, adaptiveMethod, thresholdType, blockSize, C )
```

- `cv.ADAPTIVE_THRESH_MEAN_C`: The threshold value is the mean of the neighborhood area minus the constant C.
- `cv.ADAPTIVE_THRESH_GAUSSIAN_C`: The threshold value is a gaussian-weighted sum of the neighborhood values minus the constant C.

![Untitled](/images/2023-08-04/Untitled%203.png)

### Color Filtering

Display only a specific color range in the image

1. Read image as RGB image
2. Convert image to HSV image
3. Define the upper and lower bound of the color range
4. Create the mask based on the color range

### Contours

Find boundaries of objects within images

- Contours are curves joining all the continuous points along the boundaries, having the same color
1. Read image as RGB image
2. Convert image to grayscale image
3. Convert the gray image into a binary image
4. Find the contours using `cv2.findContours()` applied on the binary image
5. Process the contours (find areas, enclosing circles, perimeters, moment, and centroid)

```python
cv.findContours(	image, mode, method	)
```

![Untitled](/images/2023-08-04/Untitled%204.png)

### Compile cpp file that uses OpenCV library

Edit CMakeLists.txt

```bash
find_package(OpenCV)
include_directories(${OpenCV_INCLUDE_DIRS})
add_executable(executable_name src/cpp_file)
target_link_libraries(executable_name ${catkin_LIBRARIES})
target_link_libraries(executable_name ${OpenCV_LIBRARIES})
```