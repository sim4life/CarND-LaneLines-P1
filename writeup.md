#**Finding Lane Lines on the Road** 

##Writeup Template

###You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I applied Gaussian Blur with kernel size 5 to the gray image. After that, I applied the Canny Edge detection technique with low threshold of 50 and high threshold of 150. Then I calculated the vertices of the polygon for the region of interest. This polygon is a isosceles trapezium. Then I masked the region of interest on the image. Afterwards, I applied the Hough Line Transform on the region of interest in the image. Then I drew the lines returned by the transform on the actual image.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by finding the slope of each line and the y-intercept. Then I selected left lane line to be the one with the slope range from -0.5 to -0.8 and the right lane line with the slope range from 0.5 to 0.8. After selecting the left and the right lane lines, I found the top coordinates and the left-most and second-left-most and right-most and second-right-most coordinates respectively. Later on, I took the average of the left-most and the second-left-most and average of right-most and second-right-most lane line. This the based on the assumption the Hough Line transform selected two lines for each lane therefore an average of them was taken to make a line pass through the middle of each lane. Afterwards, the slope of averaged lane line is extrapolated to find the max x-intercept of each lane. The the two lane lines are drawn on the image.

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]
![alt text][image2]



###2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the lane lines are covered by mud or other car debris. I've yet to select white and yellow color artifacts from the image to be able to better identify the white and yellow lanes.

Another shortcoming could be when there are white concrete road patches or when the lane lines are missing. The tire screech prints on the road also confuse the algorithm. 


###3. Suggest possible improvements to your pipeline

A possible improvement would be to select specific colors; white and yellow; in the image to better identify the lane lines.

Another potential improvement could be to select specific regions based on the road type, rising or droping road.