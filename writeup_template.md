# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

[image2]: ./test_images_output/solidWhiteCurve_output.jpg "solidWhiteCurve_output"
[image3]: ./test_images_output/solidWhiteRight_output.jpg "solidWhiteRight_output"
[image4]: ./test_images_output/solidYellowCurve2_output.jpg "solidYellowCurve2_output"
[image5]: ./test_images_output/solidYellowCurve_output.jpg "solidYellowCurve_output"
[image6]: ./test_images_output/solidYellowLeft_output.jpg "solidYellowLeft_output"
[image7]: ./test_images_output/whiteCarLaneSwitch_output.jpg "whiteCarLaneSwitch_output"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

#### My Pipeline consisted of 6 steps:
1. First I converted image to grayscale using the grayscale() function.
![GrayScale][image1]

2. Then Applied Gaussian blur on the image using the gaussian_blur() function to smoothen the image using kernel size = 5.
3. Then applied Canny edge detection algorithm using canny() function with lower & high Thresholds as 50 & 150 respectively.
4. Then applied image masking technique to remove unwanted area using the region_of_interest() helper function.
5. Then to connect lines we want & eliminate other,apllied Hough transform via Open CV method. In this step we also used the draw_lines()      method to add lines over the lanes in the image and extrapolate them.
6. Last step was to merge both the modified image and the original one to produce the result using the weighted_img() function.


In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...


![solidWhiteCurve_output][image2]
![solidWhiteRight_output][image3]
![solidYellowCurve2_output][image4]
![solidYellowCurve_output][image5]
![solidYellowLeft_output][image6]
![whiteCarLaneSwitch_output][image7]


### 2. Extrapolation technique

First of all calculated the slope of the line if the x co-ordinates of the line vary. Then if the slope is negative it is a left lane line as y increases from top to bottom in an image, and if slope is positive it is a right lane line. Collect the points of lines and for each lane, calculate average slope m and b from all the points. Then, if it is a set of left lane points, plot line from x1=(y_max-b)/m, y1=y_max to x2=x_max, y2=mx_max + b. And if it is a set of right lane points, plot line from x1=x_min, y1=(x_minm)+b to x2=(y_max-b)/m, y2=y_max

### 3. Identify potential shortcomings with your current pipeline


One potential shortcoming is that when I try to run the "challenge.mp4" video, it can't be able to recognise lane lines correctly. There is a lot of flickering and wrong detection output when the road is left or right curved. Which shows that the current pipeline is not so good for curved roads.


### 4. Suggest possible improvements to your pipeline

A possible improvement would be to improve the Pipeline such that the curved lane lines are also detected correctly without any error. As the autonomous car will face all different kinds of roads, so some changes must be made to the pipeline in order to make the lane finding error free.

Another potential improvement could be to improve to change the way the co-ordinates are calculated for extrapolation.
