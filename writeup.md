# **Finding Lane Lines on the Road** 

### Reflection

### 1. Pipeline

The main pipeline is implemented in the plot_lanes() funcion, and consists of 6 main steps: 

1. Turn image into grayscale for simplicity. 

2. Blur the image, to remove some of the noise. 

3. Apply the Canny edge detector algorithm

<img src="/result-pipeline/canny.gif" width="480" alt="Combined Image" />

4. Mask the detected edges for left and right lanes, using a polygon for parameters for the mask. 

<img src="/result-pipeline/mask.gif" width="480" alt="Combined Image" />

5. Find the lane lines - *detect_lanes()* function. 

This step was implemented inside the detect_lanes() function. First, it uses the hough transform algorithm to find some set of lines that can be drawn from the edges found. 

<img src="/result-pipeline/hough_lines.gif" width="480" alt="Combined Image" />

The goal is to find lane lanes. Many of those lines are horizontal, which is not interesting, so we get the slope of every line and filter out those that are below a certain value. Only more vertical lines will remain. 

<img src="/result-pipeline/hough_lines_filtered.gif" width="480" alt="Combined Image" />

Finally, the resulting lines are fit to parameters A and B, given y = Ax + B. Lines with similar parameters are averaged together, while those that are different are counted as different lines. The parameters that took most lines into account is selected as the ideal lane line - i.e., the average line which most lines fell onto. 

This process is repeated for left and right lanes. 

6. The lanes are plotted onto the image using a weighted sum function of images. 

<img src="/result-pipeline/result_challenge.gif" width="480" alt="Combined Image" />

### 2. Potential Shortcomings 


The results are interesting, but they are far from ideal. In some cases, specially when there is little contrast between the lane segments and asphalt, edges might not be detected so well, and so the hough lines algorithm often fails to recognize desired lines. 

If we lower the threshold for edges detection, though, or even lower constraints of hough lines algorithm, undesired lines start to be plotted, specially when there is shadow or other adversities. 


### 3. Suggest possible improvements to your pipeline

An interesting approach would be to increase image constrast for some colors (e.g., yellow) while lowering the lightness of shades of gray bellow a certain threshold (aiming at removing shadows on the road or other artifacts that aren't lane lines). 

Applying some sort of time constraint to the output would also help smoothing it, diminishing some of the abrupt variations. 
