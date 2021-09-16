---
title: Image Processing Assignment 2
date: 2021-06-21
author_profile: false
tagline: ""
header:
  overlay_image: https://github.com/tazwar70/Image-Processing-Assignment-2/raw/main/Images/test1.jpg
  overlay_filter: rgba(0,128,128,0.5)
  teaser: https://github.com/tazwar70/Image-Processing-Assignment-2/raw/main/Images/line_detection_hough_transform.jpg
toc: true
toc_label: "Contents"
toc_icon: "cog"
toc_sticky: true
tags:
- MATLAB

gallery:
  - url: https://github.com/tazwar70/Image-Processing-Assignment-2/raw/main/Images/circle_detection_r_20.jpg
    image_path: https://github.com/tazwar70/Image-Processing-Assignment-2/raw/main/Images/circle_detection_r_20.jpg
    alt: "circle_detection_r_20.jpg"
    title: "Circle Detection - Radius 20"
  - url: https://github.com/tazwar70/Image-Processing-Assignment-2/raw/main/Images/circle_detection_r_25.jpg
    image_path: https://github.com/tazwar70/Image-Processing-Assignment-2/raw/main/Images/circle_detection_r_25.jpg
    alt: "circle_detection_r_25.jpg"
    title: "Circle Detection - Radius 25"
  - url: https://github.com/tazwar70/Image-Processing-Assignment-2/raw/main/Images/circle_detection_r_30.jpg
    image_path: https://github.com/tazwar70/Image-Processing-Assignment-2/raw/main/Images/circle_detection_r_30.jpg
    alt: "circle_detection_r_30.jpg"
    title: "Circle Detection - Radius 30"
  - url: https://github.com/tazwar70/Image-Processing-Assignment-2/raw/main/Images/circle_detection_r_35.jpg
    image_path: https://github.com/tazwar70/Image-Processing-Assignment-2/raw/main/Images/circle_detection_r_35.jpg
    alt: "circle_detection_r_35.jpg"
    title: "Circle Detection - Radius 35"
  - url: https://github.com/tazwar70/Image-Processing-Assignment-2/raw/main/Images/circle_detection_r_40.jpg
    image_path: https://github.com/tazwar70/Image-Processing-Assignment-2/raw/main/Images/circle_detection_r_40.jpg
    alt: "circle_detection_r_40.jpg"
    title: "Circle Detection - Radius 40"
---

This is 2 of 3 Image Processing Assignment from my Automotive Sensor System from the University of Windsor.

# Hough Transform

## Line Detection

### Original Image

For the line detection for the Hough Transform, the following image was used,

{% include figure image_path="https://github.com/tazwar70/Image-Processing-Assignment-2/raw/main/Images/test1.jpg" 
alt="Test Image 1" 
caption="Test Image 1" 
%}

The goal was to create a function to detect the longest line from an input image.

### Comparing the Input Image

```python
% Reading the Image
image = imread('test1.jpg');
% Convert to grayscale
image_gray = rgb2gray(image);
% Edge Detection
image_edge = edge(image_gray,'canny');
% Images
subplot(1,3,1),imshow(image),title('Raw Image')
subplot(1,3,2),imshow(image_gray),title('Gray Image')
subplot(1,3,3),imshow(image_edge),title('Edge Detected Image')
```

{% include figure image_path="https://github.com/tazwar70/Image-Processing-Assignment-2/raw/main/Images/image_raw%2Bgray%2Bedge.jpg" 
alt="Comparing the input image in gray and edge" 
caption="Comparing the input image in gray and edge" 
%}

### Performing Hough Transform

The function [***line_detection***](https://github.com/tazwar70/Image-Processing-Assignment-2/blob/main/line_detection.m) was used to perform and generate the image as shown below,

{% include figure image_path="https://github.com/tazwar70/Image-Processing-Assignment-2/raw/main/Images/line_detection_hough_transform.jpg" 
alt="line_detection_hough_transform" 
caption="Image Generated from Hough Transform" 
%}

### Longest Line

The following images shows the longest image generated from the Hough Transform.

{% include figure image_path="https://github.com/tazwar70/Image-Processing-Assignment-2/raw/main/Images/line_detection_longest_line.jpg" 
alt="line_detection_longest_line" 
caption="Detected Longest Line" 
%}

### All Detected Lines - Line Detection Ver. 2

The function [***line_detection_v2***](https://github.com/tazwar70/Image-Processing-Assignment-2/blob/main/line_detection_v2.m) was used to generate an image containing all lines detected from a given image input. 

Using the function the following images were generated.

{% include figure image_path="https://github.com/tazwar70/Image-Processing-Assignment-2/raw/main/Images/line_detection_v2_hough_transform.jpg" 
alt="line_detection_v2_hough_transform" 
caption="Line Detection Ver.2 - Hough Transform" 
%}

{% include figure image_path="https://github.com/tazwar70/Image-Processing-Assignment-2/raw/main/Images/line_detection_v2_detected_lines.jpg" 
alt="line_detection_v2_detected_lines" 
caption="Line Detection Ver.2 - Detected Lines" 
%}

## Circle Detection

### Original Image

For the Circle Detection, the following image was used,

{% include figure image_path="https://github.com/tazwar70/Image-Processing-Assignment-2/raw/main/Images/test2.jpg" 
alt="test image 2" 
caption="Test Image 2" 
%}

### Detecting Circles

The [circle_detection](https://github.com/tazwar70/Image-Processing-Assignment-2/blob/main/circle_detection.m) function was used to perform Hough Transform to generate images detecting circles with a certain input radius.

Using the following snippet with varied radii, the following images are generated, with radius 20, 25, 30, 35 and 40.

```
>> circle_detection(imread('test2.jpg'),radius)
```

{% include gallery caption="Detected Circles" %}

***Note**: All MATLAB files are available on my github repo*

GitHub: [Image Processing Assignment - 2](https://github.com/tazwar70/Image-Processing-Assignment-2)
