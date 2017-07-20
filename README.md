# CarND-Term1-Project1-Lane-Finding

This is my first project in Term 1 of the Udacity Self-Driving Car Nanodegree.

I installed Docker and am using the Jupyter Notebook for this project (for
Mac users I would recommend the former in the absence of a GPU), as future projects
benefit from considerable speed-up when using Docker with Amazon Web Services
Elastic Cloud Compute (AWS EC2). This is due to the fact that GPUs massively
increase performance of neural networks, something I will be creating in the near future.

The code does the following:

 * Read an image from a video, convert to grayscale
 * Smoothen gray image using Gaussian kernel
 * Perform the Canny Function to detect edges
 * Mask a subset of the edges
 * Apply the Hough Transform to detect lines
 * Draw the lines
 * Display the result!

The Jupyter notebook (love it by the way!) you're looking for is P1 in 'submission'. Enjoy!
