---
title: Image Processing Assignment 3
date: 2021-08-21
author_profile: false
tagline: ""
header:
  overlay_image: https://github.com/tazwar70/Image-Processing-Assignment-3/raw/main/Images/3e_combined_images_rotated.jpg
  overlay_filter: rgba(0,128,128,0.5)
  teaser: https://github.com/tazwar70/Image-Processing-Assignment-3/raw/main/Images/3e_combined_images_rotated.jpg
toc: true
toc_label: "Contents"
toc_icon: "cog"
toc_sticky: true
tags:
- MATLAB

---

This is 3 of 3 Image Processing Assignment from my Automotive Sensor System from the University of Windsor.

# 3D to 2D Projection

The goal of this project is to create a function for 3D to 2D Image Projection and it is done so in 5 parts from A to E.

## Part A

Part A is for a function that will take input a set of 3D point and return an output a set of 2D points using the perspective camera model.

### The Input

For the entirity of the project, 4 3D points was used with their coordinates being,

> (-1, 0, 2), (1, 0, 5), (0, 1, 4) and (0, -1, 3)

```
p1 = [-1 0 2];
p2 = [1 0 5];
p3 = [0 1 4];
p4 = [0 -1 3];
O = [p1' p2' p3' p4'];
```

The camera is also considered to be at a focal point (0,0,0) with focal length of 1 and the image plane being ***z = 1***.

### The Function

In order to find the projected image in 2D the following function was used to find the points.

```
function object_2d = perspective_camera(O)
    % Focal Length
    focal_length = 1;
    Z = O(3,:);
    X_2d = focal_length*(O(1,:)./Z);
    Y_2d = focal_length*(O(2,:)./Z);
    object_2d = [X_2d;Y_2d];
end
```

### The Output

Using the following snippet the following coordinates were received,

```
>> perspective_camera(O)

    ans =
        -0.5000 0.2000 0 0
        0 0 0.2500 -0.3333
```

## Part B

The goal of part b is find the weak perspective projection from the original input points.

### The Function

The following function was used with the same original set of points as input,

```
function O_2d = weak_perspective_camera(O)
    % Focal Length
    focal_length = 1;
    X = focal_length*O(1,:);
    Y = focal_length*O(2,:);
    Z_0 = mean(O(3,:));
    O_2d = [X./Z_0;Y./Z_0];
end
```

### The Output

```
>> weak_perspective_camera(O)

ans =
    -0.2857 0.2857 0 0
    0 0 0.2857 -0.2857
```

## Part C

The goal of part C is to test out the functions and plot the projections and compare the plots.

### The Function

In order to perform perspective and weak perspective camera projections and generate the plots, the function [***assignment 3c***](https://github.com/tazwar70/Image-Processing-Assignment-3/blob/main/assignment_3c.m) was used.

### The Output

Running the function [***assignment 3c***](https://github.com/tazwar70/Image-Processing-Assignment-3/blob/main/assignment_3c.m) generates the following points

```
perspective_object =
    -0.5000 0.2000 0 0
    0 0 0.2500 -0.3333
```

```
weak_perspective_object =
    -0.2857 0.2857 0 0
    0 0 0.2857 -0.2857
```

{% include figure image_path="https://github.com/tazwar70/Image-Processing-Assignment-3/raw/main/Images/3c_combined.jpg" 
alt="3c_combined" 
caption="Perspective and Weak Perspective Combined Plots" 
%}

{% include figure image_path="https://github.com/tazwar70/Image-Processing-Assignment-3/raw/main/Images/3c_combined_subplot.jpg" 
alt="3c_combined_subplot" 
caption="Perspective and Weak Perspective Combined Plots" 
%}

## Part D

The goal of part D is to write a function compute the Sum of Square Differences (SSD) between the two projections.

### The Function

The function [***assignment 3d***](https://github.com/tazwar70/Image-Processing-Assignment-3/blob/main/assignment_3d.m) was used to compute the SSD from the projections.

```
function SSD = sum_of_square_differences(O)
    % P (p1, p2, p3, ...., pn)
    p = perspective_camera(O);
    % Q (p1, p2, p3, ...., pn)
    q = weak_perspective_camera(O);
    % Sum of squares differences
    SSD = sum(sum(abs(double(p)-double(q)).^2));
end
```

## Part E

The goal of part E is to make a function to rotate the input object clockwise by 45 degrees.

### The Function

The function [***assignment 3e***](https://github.com/tazwar70/Image-Processing-Assignment-3/blob/main/assignment_3e.m) was used for this part.

### The Output

Running the function provides with the following

{% include figure image_path="https://github.com/tazwar70/Image-Processing-Assignment-3/raw/main/Images/3e_combined_images_rotated.jpg" 
alt="3e_combined_images_rotated" 
caption="Combined Rotated Images" 
%}

```python
ssd_object_O =
    0.0568

ssd_object_O_R =
    0.0568

ans =
    1.3878e-17
```

***Note**: All MATLAB files are available on my github repo*

GitHub: [Image Processing Assignment - 3](https://github.com/tazwar70/Image-Processing-Assignment-3)
