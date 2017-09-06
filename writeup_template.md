# **Finding Lane Lines on the Road** 
## Writeup
The goal is to identify the left and right line lanes on the road using pre-recorded video clips. The pipeline could be able to work with real-time streams as well but it out of scope in this project. All three video clips are daytime and colour recordings but the resolutions differ. I created a pipeline that identifies which resolution is used and adapts to it automatically so it can be used freely with ANY of the three given test clips.

[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

The video clip is handled as a series of images. The processing pipeline runs on every image but the algorithm creates a statistics about the lanes' position and heading. This way it is not a big problem if temporarily the lines cannot be detected because the algorithm takes the best guess based on past results. The error should be marginal in most of the cases as the change of the lanes' position on a stream of images should be continuous (if the camera is working properly which I assumed). 

### 1. The pipeline

The processing is done in the class line_detector. A helper class line_stats is used to keep track of both lanes' position and heading between images as well as for creating statistics of the Hough line pieces (thus making a good guess of its location) while processing a single image. 

My pipeline consists of the following steps:

1-4. Doing the image processing steps (convert to grayscale, call Canny transform, mark ROI, calling the Hough transform)

5. The draw_lines() function is responsible for drawing two solid lines inside the ROI which is predefined by vertices for both resolutions. The function creates a statistics on both the left and the right lanes by segmenting the left from the right based on the sign of the slope of the given piece: if it is positive, the piece is probably part of the right lane, if negative, probably of the left. I used the term probably as on noisy images this is not necessarily the case. I found that by eliminating the pieces with slope greater than 2 (more than 45 degrees difference from the vertical) most of the noise (shadows, different materials of concrete/tarmac) can be filtered out. The real trick is, however, that the function does not draw the lanes based on the stats of the actual image. It is used only to update the global statistics which keeps track of the lanes between images. After the update the lines are drawn based on the average of the weighted sum of the last images.

6. The results are given by creating a weighted image of the original input and the result of the draw_lines function.

### 2. Potential shortcomings

If no lane lines can be detected for a long time the statistics might go off and divert from the actual position. When using the detector this case must be handled accordingly (perhaps by assigning lower/degrading confidence to these).

### 3. Possible improvements

At the moment the vertices are hard-coded in the class which is not right. It should be assigned as an external parameter but for the sake of convinience in the testing/validating I choose to do it this way (but the set_roi function is also implemented and can be called by the user).
