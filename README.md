# Finding Lane Lines on a Road
The goal of this project is to be able to read images/videos and annotate lane lines on the road.
---

## Steps
(If the input is a video, firstly the pipeline converts each frame to the BGR color space for use in OpenCV)
1. I split the given image into seperate BGR channels and identified that the red channel best showed both the white and yellow lanes.
<img src="./steps/1.png"/>

2. I isolated the red channel and applied gaussian blur.
<img src="./steps/2.png"/>

3. I then ran the Canny Edge detection algorithm on the processed image.
<img src="./steps/3.png"/>

4. I then found all the hough lines in the edge detection image and modified the draw_lines function to identify each lane.

## draw_lines()
The modified draw_lines function starts of by identifying what line segments are part of the left lane marking and the right lane marking. This is done by calculating the slope and stating that all lines with a slope of more than 0 are part of the right, and the lines with a slope of less than 0 are part of the left.

Afterwards, it calculates the average slope and mid-point of both the left and right line segments. It also keeps track of the line segment with the highest y position as that is the top of the lane.

After finding the average mid-point of each lane marking, it uses the slope to calculate the line equation of each lane and uses the line equation to find the x,y coordinates of the lane at the bottom of the image and the highest detected y position of the lane. Afterwards a thick line is drawn between those two points.
<img src="./steps/4.png"/>
