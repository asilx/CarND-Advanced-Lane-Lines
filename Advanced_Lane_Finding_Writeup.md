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

### Lane Finding Pipeline for Images
