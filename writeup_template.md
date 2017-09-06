# **Finding Lane Lines on the Road** 
## Writeup
The goal is to identify the left and right line lanes on the road using pre-recorded video clips. The pipeline could be able to work with real-time streams as well but it out of scope in this project. All three video clips are daytime and colour recordings but the resolutions differ. I created a pipeline that identifies which resolution is used and adapts to it automatically so it can be used freely with any of the three given test clips.

[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. The pipeline

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I .... 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
