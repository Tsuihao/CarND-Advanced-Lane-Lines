## Writeup 
---

**Advanced Lane Finding Project**

The goals / steps of this project are the following:

* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
* Apply a distortion correction to raw images.
* Use color transforms, gradients, etc., to create a thresholded binary image.
* Apply a perspective transform to rectify binary image ("birds-eye view").
* Detect lane pixels and fit to find the lane boundary.
* Determine the curvature of the lane and vehicle position with respect to center.
* Warp the detected lane boundaries back onto the original image.
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.

[//]: # (Image References)

[camera_cali]: ./output_images/camera_cali.PNG
[undistorted_img]: ./output_images/undistorted_img.PNG
[image_filter]: ./output_images/image_filter.PNG
[warped_img]: ./output_images/warped_img.PNG
[image5]: ./examples/color_fit_lines.jpg "Fit Visual"
[final_img]: ./output_images/final_img.PNG
[video1]: ./project_video.mp4 "Video"

### Requirement: [Rubric](https://review.udacity.com/#!/rubrics/571/view) Points

---

### Camera Calibration

#### 1. Briefly state how you computed the camera matrix and distortion coefficients. Provide an example of a distortion corrected calibration image.

The code for this step is contained in the first code cell of the [IPython notebook](https://github.com/Tsuihao/CarND-Advanced-Lane-Lines/blob/master/Advaned_lane_line.ipynb)

I start by preparing "object points", which will be the (x, y, z) coordinates of the chessboard corners in the world. Here I am assuming the chessboard is fixed on the (x, y) plane at z=0, such that the object points are the same for each calibration image.  Thus, `objp` is just a replicated array of coordinates, and `objpoints` will be appended with a copy of it every time I successfully detect all chessboard corners in a test image.  `imgpoints` will be appended with the (x, y) pixel position of each of the corners in the image plane with each successful chessboard detection.  

I then used the output `objpoints` and `imgpoints` to compute the camera calibration and distortion coefficients using the `cv2.calibrateCamera()` function.  I applied this distortion correction to the test image using the `cv2.undistort()` function and obtained this result: 

![alt text][camera_cali]

### Pipeline (single images)

#### 1. Provide an example of a distortion-corrected image.

The below image shows the orginal image and the undistorted image.
![alt text][undistorted_img]

#### 2. Describe how (and identify where in your code) you used color transforms, gradients or other methods to create a thresholded binary image.  Provide an example of a binary image result.

Please refer to the class 
```python
class ImageFilter

def apply
```
in the [IPython notebook](https://github.com/Tsuihao/CarND-Advanced-Lane-Lines/blob/master/Advaned_lane_line.ipynb). I have used the LAB color space and sobel operation (with gaussian blur) to filter the image. The result can be seen in the figure below. 


**PS**: I have tried different combination of filtering. e.g: HLS color space, sobel in gradient, sobel in magnitude, etc. This step consumes the majority of time in this project. It reveals that the traditional computer vision approach of lane finding (comparing to CNN) requires a lot of artifical parameter tuning in terms of "explicitly telling which object we are looking for". 

![alt text][image_filter]

#### 3. Describe how (and identify where in your code) you performed a perspective transform and provide an example of a transformed image.
 

In the [IPython notebook](https://github.com/Tsuihao/CarND-Advanced-Lane-Lines/blob/master/Advaned_lane_line.ipynb)
```python
class PerspectiveTransform

def transform(self, image, M):
```

The `transform()` function takes as inputs an image (`img`)and a transformation matrix (`M`) . The transformation matrix is based on the hard-coded value in the calss:

```python
src=np.float32([[572, 450], 
                [0, 720], 
                [1280, 720],
                [702, 450]])

dst=np.float32([[160, 0], 
                [160, 720], 
                [1120, 720], 
                [1000, 0]])
```

This resulted in the following source and destination points:

| Source        | Destination   | 
|:-------------:|:-------------:| 
| 572, 450      | 160, 0        | 
| 0, 720        | 160, 720     |
| 1280, 720     | 1120, 720      |
| 702, 450      | 1000, 0        |


![alt text][warped_img]

#### 4. Describe how (and identify where in your code) you identified lane-line pixels and fit their positions with a polynomial?

Then I did some other stuff and fit my lane lines with a 2nd order polynomial kinda like this:

![alt text][image5]

#### 5. Describe how (and identify where in your code) you calculated the radius of curvature of the lane and the position of the vehicle with respect to center.

In the [IPython notebook](https://github.com/Tsuihao/CarND-Advanced-Lane-Lines/blob/master/Advaned_lane_line.ipynb)
```python
class LaneLineFinder

def get_lane_geometry
```
I calculate the radius of the line and the center departure based on this [reference](https://www.intmath.com/applications-differentiation/8-radius-curvature.php).

#### 6. Provide an example image of your result plotted back down onto the road such that the lane area is identified clearly.

In the [IPython notebook](https://github.com/Tsuihao/CarND-Advanced-Lane-Lines/blob/master/Advaned_lane_line.ipynb)
```python
class ImageLaneDetector

def apply
```
The class ImageLaneDetector is a host calss which includes the sub class (camera_calibrator, image_filter, image_transformer, lane_line_finder)

![alt text][final_img]

---

### Pipeline (video)

#### 1. Provide a link to your final video output.  Your pipeline should perform reasonably well on the entire project video (wobbly lines are ok but no catastrophic failures that would cause the car to drive off the road!).

Here's a [link to my video result](https://www.youtube.com/watch?v=uJ7xPukCM28&index=3&list=PL5Q1QlXB5Rp8u5mwFbCur1_boPTTFsu_L&t=0s)

---

### Discussion

#### 1. Briefly discuss any problems / issues you faced in your implementation of this project.  Where will your pipeline likely fail?  What could you do to make it more robust?

* Imagefilter is still not optimal (e.g. Color space and sobel operation combinations)
* The implementation heavily affect by the Warped area as well (e.g. For chellenge_video and harder_challenge_video, different warped area should be used)
* The current implementaion is still not stable in terms of the [video time stamp 21s](https://youtu.be/uJ7xPukCM28?t=21s), this should be improved soon