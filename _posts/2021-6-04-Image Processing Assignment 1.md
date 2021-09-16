---
title: Image Processing Assignment 1
date: 2021-06-04
author_profile: false
tagline: ""
header:
  overlay_image: https://github.com/tazwar70/Image-processing-assignment-1/raw/main/Images/edge-detection-with-varried-noise-with-rmse.jpg
  overlay_filter: rgba(0,128,128,0.5)
  teaser: https://github.com/tazwar70/Image-processing-assignment-1/raw/main/Images/edge-detection-with-varried-noise-with-rmse.jpg
toc: true
toc_label: "Contents"
toc_icon: "cog"
toc_sticky: true
tags:
- MATLAB
---

This is 1 of 3 Image Processing Assignment from my Automotive Sensor System from the University of Windsor.

## The Original Image

The image used for the entire project is a picture of Lena.

{% include figure image_path="https://raw.githubusercontent.com/tazwar70/Image-processing-assignment-1/main/Images/lena.bmp" 
alt="Lena" 
caption="Lena" 
%}

## Task 1 - Finding the Root Mean Square Error

The following table shows the quantitative analysis between 4 different Edge Detection methods with 5 different variance levels of Gaussian noise compared to a reference image using the Root Mean Squared Error as the performance method. The reference image used is 'lena.bmp' with Canny edge detection with threshold = 0.1, sigma = 1.


<table>
<thead>
	<tr>
		<th>Noise\ Edge</th>
		<th>Sobel</th>
		<th>Prewitt</th>
		<th>LoG</th>
		<th>Canny</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>0.01</td>
		<td>0.2955</td>
		<td>0.2956</td>
		<td>0.3860</td>
		<td>0.4376</td>
	</tr>
	<tr>
		<td>0.05</td>
		<td>0.3186</td>
		<td>0.3178</td>
		<td>0.4558</td>
		<td>0.5363</td>
	</tr>
	<tr>
		<td>0.1</td>
		<td>0.3199</td>
		<td>0.3201</td>
		<td>0.4763</td>
		<td>0.5605</td>
	</tr>
	<tr>
		<td>0.5</td>
		<td>0.3138</td>
		<td>0.3136</td>
		<td>0.4955</td>
		<td>0.5863</td>
	</tr>
	<tr>
		<td>1</td>
		<td>0.3113</td>
		<td>0.3113</td>
		<td>0.4976</td>
		<td>0.5928</td>
	</tr>
</tbody>
</table>

The following images show the difference between Sobel, Prewitt, Laplacian of Gaussian and Canny edge detection with varying levels of Gaussian noise.

{% include figure image_path="https://github.com/tazwar70/Image-processing-assignment-1/raw/main/Images/edge-detection-with-varried-noise-with-rmse.jpg" 
alt="edge-detection-with-varried-noise-with-rmse" 
caption="Edge Detection with varried noise with RMSE" 
%}

## Task 2 - Performance Analysis of Canny Edge Detector

To qualitatively analyze the performance of the Canny Edge Detection method with varied threshold, initially, the threshold range needs to be found.

{% include figure image_path="https://github.com/tazwar70/Image-processing-assignment-1/raw/main/Images/canny_with_threshold_0.jpg" 
alt="canny_with_threshold_0" 
caption="Canny Edge Detection with threshold at 0" 
%}

Testing it with a threshold of 1 using the following snippet will result with an error.

```python
% Reading Image
img = imread('lena.bmp');
imshow(edge(img,'Canny',1)),title('Canny - threshold = 1')
```

Therefore, in order to analyze the performance of the Canny Edge Detector, the threshold range needs to be 0 ≤ t < 1.
The following snippet was used to analyze the performance of the Canny Edge Detector with varied thresholds.

```python
% Reading Image
img = imread('lena.bmp');
% Canny Edge Detection over a range of thresholds
z=0;y=0;
for x = [0 0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 0.99 0.999]
    z = z+1;
    subplot(3,4,z),imshow(edge(img,'Canny',x)),title("Canny - Threshold = " + num2str(x))
end
```

{% include figure image_path="https://github.com/tazwar70/Image-processing-assignment-1/raw/main/Images/canny_with_varied_threshold.jpg" 
alt="canny_with_varied_threshold" 
caption="Canny with Varried Threshold" 
%}

## Task 3 - Testing the strength of Canny Edge Detection

To understand the strength of the Canny Edge Detection, at first Canny was tested with other methods at their default values.

```python
img = imread('lena.bmp');
subplot(1,4,1),imshow(edge(img,'Canny')),title('Canny')
subplot(1,4,2),imshow(edge(img,'Sobel')),title('Sobel')
subplot(1,4,3),imshow(edge(img,'Prewitt')),title('Prewitt')
subplot(1,4,4),imshow(edge(img,'log')),title('LoG')
```

{% include figure image_path="https://github.com/tazwar70/Image-processing-assignment-1/raw/main/Images/edge_detection_default_settings.jpg" 
alt="edge_detection_default_settings" 
caption="Edge Detection with Default Settings" 
%}

To further compare them, the threshold values are compared with the range 0 - 0.5.
Initially checking the difference with the threshold set at 0.

```python
% Reading Image
img = imread('lena.bmp');
 
subplot(1,4,1),imshow(edge(img,'Canny',0)),title('Canny - threshold = 0')
subplot(1,4,2),imshow(edge(img,'Sobel',0)),title('Sobel - threshold = 0')
subplot(1,4,3),imshow(edge(img,'Prewitt',0)),title('Prewitt - threshold = 0')
subplot(1,4,4),imshow(edge(img,'log',0)),title('LoG - threshold = 0')
```

{% include figure image_path="https://github.com/tazwar70/Image-processing-assignment-1/raw/main/Images/edge_detection_with_no_threshold.jpg" 
alt="edge_detection_with_no_threshold" 
caption="Edge Detection with no threshold" 
%}

Checking the difference with threshold set at 0.1, 0.2, 0.3, 0.4 and 0.5.

{% include figure image_path="https://github.com/tazwar70/Image-processing-assignment-1/raw/main/Images/edge_detection_with_varried_threshold_v1.jpg" 
alt="edge_detection_with_varried_threshold" 
caption="Edge Detection with varried threshold" 
%}

From the two sets of images generated it can be seen that the Canny method is capable of more clearly distinguishing the edges the image can be more fine-tuned. From the images with the threshold set to 0, it is visible that the image produced with the Canny edge detection is more defined compared to the other methods. Similarly, when checking over the range 0.1 – 0.5, it can be seen that the other methods fail to define the image especially the Laplacian of Gaussian method. As for a noisy image, the following shows with increasing noise, Canny loses the ability to trace out the object.

{% include figure image_path="https://github.com/tazwar70/Image-processing-assignment-1/raw/main/Images/canny_with_varied_noise.jpg" 
alt="canny_with_varied_noise" 
caption="Canny Edge Detectiopn with varied noise" 
%}

## Task 4 - Why directional edge detectors perform better in the images of unconstrained natural environment?

For an edge detection algorithm to function optimally, the object needs to be in focus with good separation between the background and the foreground. Unconstrained natural environment means a scenario where an image can be produced with proper lighting, no noise and a clear separation between the foreground and the background with the object. As seen in the image samples above, with increasing noise, Canny slowly loses the ability to distinguish the object.

The following shows the Canny edge detection method compared to a noisy image and a denoised image. For the purpose of testing default MATLAB parameters were used.

{% include figure image_path="https://github.com/tazwar70/Image-processing-assignment-1/raw/main/Images/Canny_on_Denoised_Image.jpg" 
alt="Canny_on_Denoised_Image" 
caption="Canny on Denoised Image" 
%}

This comparison clearly shows that for a clear natural image, the edge detection method performs the best. The second column images show a noisy image with the edge detection method is unable to trace the image at all. The third column shows a denoised image along with another image with edge detection applied, where the edges were somewhat traced. Hence, directional edge detectors perform better in the images of unconstrained natural environment.

***Note**: All MATLAB files are available on my github repo*

GitHub: [Image Processing Assignment - 1](https://github.com/tazwar70/Image-processing-assignment-1)
