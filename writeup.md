# **Finding Lane Lines on the Road** 

## Sara Collins

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

[grey_image]: ./test_image_output/grey_solidYellowLeft.jpg "Grayscale"
[canny_image]: ./test_image_output/canny_solidYellowLeft.jpg "Canny"
[gauss_image]: ./test_image_output/blurred_solidYellowLeft.jpg "Gaussian Blur"
[masked_image]: ./test_image_output/masked_solidYellowLeft.jpg "Masked"
[hough_image]: ./test_image_output/hough_solidYellowLeft.jpg "Hough"
[weighted_image]: ./test_image_output/weighted_solidYellowLeft.jpg "Weighted"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.
The pipeline for processing the images to identify lane lines consists of six steps:  
* **Grayscale**: Conversion of the input image from color to gray tones.  
![Grayscale Image][grey_image]
* **Canny Edge Detection**: The grayscale image is then taken and run through OpenCV's Canny edge detection algorithm.  
![Canny Image][canny_image]
* **Gaussian Blur**: Gaussian blur is then applied to the canny edge-detected image.  
![Gaussian_Blur_Image][gauss_image]
* **Masking - Region of Interest**: A mask is applied over all but a triangle shape in the lowest portion of the Gaussian-blurred image.  
![Masked Image][masked_image]
* **Hough Lines**: Finds primary lines for drawing lane lines.  
![Hough_Image][hough_image]
* **Weighted Lines**: Weighting lane lines so they show up thicker on the image.  
![Weighted Lines Image][weighted_image]

In the first portion of the project, I simply left the initial drawLines() function as it was to draw out all line segments returned from the Hough lines function. However, while this identified line segments quite well, it did not provide a solid line over a dashed lane line, and as it was, also kept all line segments regardless of their slope, including some horizontal line segments at both the horizon and in the reflection of the windshield.  
In order to draw a solid line on the image over the dashed lane line and eliminate extraneous lines with slopes that were not within the range of angles typically found in the lane lines, and also calculated the intercept for each line segment. From there, added the line point list and individual x or y list for the left lane if the slope was less than the negation of a slope threshold parameter, and to lists for the right lane if the slope was greater than the slope threshold parameter.  
Next, I fit all the x and y points to lines for both the left and right lane line using the np.polyfit function, calling the slope and intercept both 1 if the lines did not exist (this was necessary for some image frames in the video segment where edges were not adequately detected to form the lane line.  
After that, I found the 'y' values for the endpoints for both lane lines, since they were going to be the same, thus resulting in the lines being of even length. I also shortened the lines a bit so they didn't collide with one another. From there, I extrapolated the lines by subtracting the intercepts from the y values for each line, and then dividing that calculation by the slope for each respective line.  Lastly, both the left and right lines were drawn in the same fashion as they were in the original function. 

### 2. Identify potential shortcomings with your current pipeline


A shortcoming of this approach is that it doesn't handle curves very well, and definitely does not see things particularly far along down the road. 

Another shortcoming could be roadways that turn or curve outside of the region of interest, and roads that don't have lane lines at all or are very indistinct. 

Also, wet roadways that are highly reflective, and roadways covered with snow or other precipitation or sediment would also prove to be major issues for this particular approach. 


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
