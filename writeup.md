# **Finding Lane Lines on the Road** 

### Reflection

### 1. Pipeline

The main pipeline is implemented in the plot_lanes() funcion, and consists of 6 main steps: 

1. Turn image into grayscale for simplicity. 

2. Blur the image, to remove some of the noise. 

3. Apply the Canny edge detector algorithm

![alt text][result-pipeline/canny.gif]

4. Mask the detected edges for left and right lanes, using a polygon for parameters for the mask. 

![alt text][result-pipeline/mask.gif]

5. Find the lane lines - *detect_lanes()* function. 

This step was implemented inside the detect_lanes() function. First, it uses the hough transform algorithm to find some set of lines that can be draw from the edges found. 

![alt text][result-pipeline/hough_lines.gif]

The goal is to find lane lanes. Many of those lines are horizontal, which is not interesting, so we get the slope of every line and filter out those that are below a certain value. Only more vertical lines will remain. 

![alt text][result-pipeline/hough_lines_filtered.gif]

### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
