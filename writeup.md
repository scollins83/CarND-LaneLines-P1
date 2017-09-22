# **Finding Lane Lines on the Road** 

## Sara Collins

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.
The pipeline for processing the images to identify lane lines consists of six steps:  
* **Grayscale**: Conversion of the input image from color to gray tones.
* **Canny Edge Detection**: The grayscale image is then taken and run through OpenCV's Canny edge detection algorithm.
* **Gaussian Blur**: Gaussian blur is then applied to the canny edge-detected image.
* **Masking - Region of Interest**: A mask is applied over all but a triangle shape in the lowest portion of the Gaussian-blurred image. 
* **Hough Lines**: Finds primary lines for drawing lane lines. 
* **Weighted Lines**: Weighting lane lines so they show up thicker on the image. 

In the first portion of the project, I simply left the initial function 

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
