# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./for_writeup/canny_edge.png "canny edge detected image"
[image2]: ./for_writeup/region_of_interest.png "region of interest"
[image3]: ./for_writeup/line_image.png "line drawn image"
[image4]: ./test_images_output/solidWhiteCurve.jpg.png "final image"

---

### Reflection

### 1. Description of my pipeline

My pipeline consisted of 7 steps:
1. in this section the image is converted to grayscale
2. gaussian blur is applied
3. canny edge detection is used to extract possible lines (a demo output is shown below)
![alt text][image1]
4. Since even after the canny edge detection there is a lot of area that is detected and since we know that there are some areas  where the lane line just can't be we will apply a mask to extract region of interest. (a demo output is shown below)
![alt text][image2]
5. Hough tranform is applied to extract straight lines from the region of interest.
6. This gives us a set of points using which the lines can be drawn. We first threshold the x values along the centre of the image and separate the left and right lane lines. Then for each set we use numpy's polyfit function with degree 1 to fit the straight line through those points. This gives us the slope and intercept. We take y1 and y2 to be the bottom of the image and the top of the region of interest, from this we compute its x values and generate a nice complete line. (a demo output is shown below)
NOTE: These images were taken before this was fully implimented
![alt text][image3]
7. Now the lines drawn on the image are added to the original image to get the final output(a demo output is shown below)
![alt text][image4]


### 2. Potential shortcomings with the current pipeline


One potential shortcoming would be what would happen when the the view is not clear like in the challenge video.

Another shortcoming could be that since I am using a linear interpolation if the car is turning we will not get a curved path.

Another shortcoming could be that when there is a car in front it may not detect the line properly or if there is an intersection.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to run the pipeline in a different colorspace that is capable of handling variations in the environment.

Another potential improvement could be use other machine learning based algorithm to detect lines so that it can be done in every environment.
