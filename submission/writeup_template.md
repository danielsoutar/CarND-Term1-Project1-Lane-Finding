# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./images/exit-ramp.jpg
[image2]: ../images/paleRoad.jpg


---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consists of 6 steps, executed as follows:

* First I converted the image(s) to grayscale. Colour is not necessary for our purposes - we are only trying to draw lines indendently of the colour of the lane lines. Plus, processing colour is expensive.

* Then I apply the canny function, a clever algorithm that smoothes the images so that noise in the image is tuned out. The gradient of a given pixel is compared with its surroundings.

* Then I apply a 'mask' (i.e. I select a portion of the image to analyse). This is so that I can focus my remaining computation more effectively. I did consider applying the mask first, but some lovely gentleman on Stack Overflow pointed out that this would lead to a 'frame' around the mask and ruin the Canny function.

* Then I apply the probabilistic Hough transform. Roughly, the dots found by the canny function are connected by the Hough transform if they are deemed to be sufficiently 'related'. The probabilistic variant is much faster than its classical counterpart, so I used that.

* Nearly there! I then draw the lines found by the Hough transform. I calculated the slope of the lines and compared them to some standard (the average was consistently about -/+ 0.7). I use the previous frames (inspired by Esmat Anis' article on Medium) as a way of stabilising the results. One thing I tried to do differently since I looked at his code pretty carefully was attempt to handle the case when the parameters returned no lines to draw. This error-handling is good practice, although the length of the code suffered as a result.

* Finally I overlay the lines on top of the original image and display it!


### 2. Identify potential shortcomings with your current pipeline

One (actual) shortcoming was the poor performance on the challenge.mp4 video. I now realise why, or have a theory why - I use a fixed constant as the standard for allowing a slope to be added. But in a dynamic setting (i.e. a corner) that might not work. My reasoning was to stabilise the results, but I now accept that this might be why my code runs less well on the challenge video, and sharp corners in general.

I also noticed my code failed to draw any line on the image titled 'exit-ramp.jpg', displayed:

![alt text][image1]

A minor quibble is the slight offset in the following image (titled 'paleRoad.jpg'):

![alt text][image2]

I'm very new to Python, so the syntax and style is quite strange to me coming from a Java background. I do like its brevity, but I could probably have tidied up the draw_lines function a bit.

### 3. Suggest possible improvements to your pipeline

Probably try changing the 'stabilising' part of draw_lines to allow for a more dynamic result that can handle corners. One interesting idea I had was to modify the actual location of the mask itself if there were fewer than x points detected on a given side (that would be very clever - and probably very buggy!).

I also think lighting was the reason for the offset line in 'paleRoad.jpg', so maybe normalising the colour prior to gray-scaling could help. 

Ohh, one other thing - because you can have cracks in the road, or objects on it, maybe having two smaller regions would reduce noise even further.






All the same, I had a lot of fun fiddling around with code and exclaiming 'what the hell are you doing' every five minutes. It's a fun process and I'm looking forward to doing it all over again, version 2.0!

Thanks for reading!
