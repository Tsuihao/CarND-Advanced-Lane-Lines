## Advanced Lane Finding
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)


In this project, your goal is to write a software pipeline to identify the lane boundaries in a video, but the main output or product we want you to create is a detailed writeup of the project.


Check Write Up & Video
---
**[writeup](https://github.com/Tsuihao/CarND-Advanced-Lane-Lines/blob/master/writeup.md)**

**[video in HLS color space](https://www.youtube.com/watch?v=fpLCauf7KTc)** (_recommend_)

**[video in LAB color space](https://www.youtube.com/watch?v=uJ7xPukCM28)**


The Project
---

The goals / steps of this project are the following:

* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
* Apply a distortion correction to raw images.
* Use color transforms, gradients, etc., to create a thresholded binary image.
* Apply a perspective transform to rectify binary image ("birds-eye view").
* Detect lane pixels and fit to find the lane boundary.
* Determine the curvature of the lane and vehicle position with respect to center.
* Warp the detected lane boundaries back onto the original image.
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.

The images for camera calibration are stored in the folder called `camera_cal`.  The images in `test_images` are for testing your pipeline on single frames.  If you want to extract more test images from the videos, you can simply use an image writing method like `cv2.imwrite()`, i.e., you can read the video in frame by frame as usual, and for frames you want to save for later you can write to an image file.  

To help the reviewer examine your work, please save examples of the output from each stage of your pipeline in the folder called `output_images`, and include a description in your writeup for the project of what each image shows.    The video called `project_video.mp4` is the video your pipeline should work well on.  

The `challenge_video.mp4` video is an extra (and optional) challenge for you if you want to test your pipeline under somewhat trickier conditions.  The `harder_challenge.mp4` video is another optional challenge and is brutal!

If you're feeling ambitious (again, totally optional though), don't stop there!  We encourage you to go out and take video of your own, calibrate your camera and show us how you would implement this project from scratch!

Review Findings
---
[First Review](https://review.udacity.com/#!/reviews/1303319)

[Second Review](https://review.udacity.com/?utm_medium=email&utm_campaign=ret_000_auto_ndxxx_submission-reviewed&utm_source=blueshift&utm_content=reviewsapp-submission-reviewed&bsft_clkid=0a858b67-173d-407c-837d-3402ef588c56&bsft_uid=1e07ff6b-26c2-40f5-8927-a5800725c305&bsft_mid=4221f4ad-6d8a-4cb9-88ee-acec37d87d92&bsft_eid=6f154690-7543-4582-9be7-e397af208dbd&bsft_txnid=d55fc274-0cad-4e0b-b26a-d42f397a1243#!/reviews/1305684)

Notes
---
Currently, the warped area (perspective transform area) is customed for the project_video.
for the challenge_video and harder_challenge_video need another warped area.