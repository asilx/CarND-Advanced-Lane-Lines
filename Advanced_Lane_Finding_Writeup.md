# Self-Driving Car Engineer Nanodegree


---

**Advanced Lane Finding Project**


## Project Goals

The goals / steps of this project are the following:

* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
* Apply a distortion correction to raw images.
* Use color transforms, gradients, etc., to create a thresholded binary image.
* Apply a perspective transform to rectify binary image ("birds-eye view").
* Detect lane pixels and fit to find the lane boundary.
* Determine the curvature of the lane and vehicle position with respect to center.
* Warp the detected lane boundaries back onto the original image.
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position

The script is located as P2.ipynb
The output folder for images and videos 


### Camera Calibration

Firstly I define a set of points (x,y,z) in the chessboard grid. The chessboard is fixed on the (x, y) plane at z=0. That means that the object points do not varry at each calibration image.  So, `objp` is just a replicated array of coordinates, and `objpoints` will be appended with a copy of it every time I successfully detect all chessboard corners in a test image.  `imgpoints` will be appended with the (x, y) pixel position of each of the corners in the image plane with each successful chessboard detection.

Using these two lists of points, OpenCV's calibrateCamera function calculates two calibration parameters namely mtx and dist

### Undistorting Images

Using two calibration parameters, mtx and dist, I am able to correct distortions at the images (Function: undistort_image)

Example chessboard image: /output_images/cal_undistorted.jpg

### Lane Finding Pipeline for Images

* Apply distortion correction to the given image (Example image: /output_images/straight_lines1_undistorted.jpg). 
* Obtain a binary threshold image resulting from gradients and color transforms (Example image: /output_images/straight_lines1_thresholded.jpg).
   Gradients are obtained by getting sobel in both x- and y-axes. Then, combining them together by finding  their absolute value and directions
   Color threshold is done in 'S' channel of HLS coding
* Apply a perspective transform to rectify binary image ("birds-eye view") (Example image: /output_images/straight_lines1_warped.jpg)
   y_bottom = 720 
   y_top = 450 
   src_x1 = 240
   zoom_out_factor = 0.55
   dest_x1 = src_x1 + (src_x2 - src_x1) * (1- zoom_out_factor) / 2 
   dest_x2 = src_x2 - (src_x2 - src_x1) * (1- zoom_out_factor) / 2
* Detect lane pixels using histograms and fit a curve using sliding windows technique. (Example image: /output_images/straight_lines1_windows.jpg)
   The first step  to split the histogram into two sides, one for each lane line
   The next step is to set a few hyperparameters related to our sliding windows, and set them up to iterate across the binary activations in the image.
