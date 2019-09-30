# **Finding Lane Lines on the Road** 
---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"
[image2]: ./test_images_output/solidYellowLeft.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps. First, I converted the images to grayscale, then I applied Gaussian smoothing, after that I found edges in blurred image by Cany Edge Detection, later I masked the edged image with a four-sided polygon, and then I used the function extrapolate() for to connect/average/extrapolate line segments instead of draw_lines() and hough_lines(), last I drew the extrapolate lines on the frame.

In order to draw a single line on the left and right lanes, I implemented the extrapolate() function. In this function, I used global variables for storing distances between them and coordinates of the left and right lines. I take stored last some values of these parameters. I used the cv2.HoughLines() function for taking rho and theta values of Hough coordinates of the lines. HoughLines() function is returning NoneType value, when sun lights enter to the camera directly or if there are no lines in an edged image. Then I made a filter for avoiding noises and NoneType error for HoughLines() function. I used 0.95 and 2.11 values of Theta for avoiding noises that other unuseful lines made. I found these values from some test photos for right and left lane lines. We can find the x coordinates of lines by using the Hough coordinates with;
                x=(rho-y*sin(theta))/cos(theta)
Next part I implemented some codes for the summing x coordinates of lines when lines are visible and also for extrapolating the invisible line parts. Later I assign x coordinates of the lines by using to last values of coordinates and draw the lines on a black canvas.

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when there is no line on the road.

Another shortcoming could be temporary lines during road repair and temporary and very close permanent lines can be found in the masked area at the same time.

The curvature of the bend can be very small.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be on extraplate() function. For example, it can divide into small specific functions.

Another potential improvement could be to figure of lines. We can draw curved lines on curved roads.

