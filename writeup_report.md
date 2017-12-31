## Project: Search and Sample Return

---


**The goals / steps of this project are the following:**

**Training / Calibration**

* Download the simulator and take data in "Training Mode"
* Test out the functions in the Jupyter Notebook provided
* Add functions to detect obstacles and samples of interest (golden rocks)
* Fill in the `process_image()` function with the appropriate image processing steps (perspective transform, color threshold etc.) to get from raw images to a map.  The `output_image` you create in this step should demonstrate that your mapping pipeline works.
* Use `moviepy` to process the images in your saved dataset with the `process_image()` function.  Include the video you produce as part of your submission.

**Autonomous Navigation / Mapping**

* Fill in the `perception_step()` function within the `perception.py` script with the appropriate image processing functions to create a map and update `Rover()` data (similar to what you did with `process_image()` in the notebook).
* Fill in the `decision_step()` function within the `decision.py` script with conditional statements that take into consideration the outputs of the `perception_step()` in deciding how to issue throttle, brake and steering commands.
* Iterate on your perception and decision function until your rover does a reasonable (need to define metric) job of navigating and mapping.

[//]: # (Image References)

[image1]: ./misc/rover_image.jpg
[image2]: ./output/rover_view_example.jpg "Rover View"
[image3]: ./calibration_images/example_grid1.jpg
[image4]: ./calibration_images/example_rock1.jpg
[image5]: ./output/warped_example.jpg "Warped Image"
[image6]: ./output/warped_mask_example.jpg "Warped Mask"
[image7]: ./output/warped_threshed.jpg "Warped Thresholded Image"
[image8]: ./output/world.jpg "World Image"
[image9]: ./output/rock.jpg "Rock Image"

## [Rubric](https://review.udacity.com/#!/rubrics/916/view) Points
### Here I will consider the rubric points individually and describe how I addressed each point in my implementation.

---

### Notebook Analysis
#### 1. Sample Rover image from different view points.

![alt text][image1]


![alt text][image2]


Calibration image:
![alt text][image3]


Rock image:
![alt text][image4]


#### 2. Perspect Transform.
Select the source and destination points to perform the transform, then use cv2.getPerspectiveTransform and cv2.warpPerspective functions to obtain the warped image and warped mask.


Warped image:
![alt text][image5]


Warped mask:
![alt text][image6]

#### 3. Color threshold.
Select the pixels with all three channels has a value greater than 160.


Thresholded image:
![alt text][image7]

#### 4. Convert pixels to world coordinates.

Sample image on upper left corner, warped image on upper right, thresholded image on lower left, and world image on lower right.

![alt text][image8]

#### 5. Find Rocks.
For an image, search for yellow pixels, that is, pixels that have greater than 110 red and green values, and lower than 50 blue value.

![alt text][image9]

#### 6. Populate the `process_image()` function.
The `process_image()` function applies the steps mentioned above.


### Autonomous Navigation and Mapping

#### 1. The `perception_step()`
The `perception_step()` function (at the bottom of the `perception.py` script) is filled as in the `process_image()` function in the Jupyter Notebook. In addition, the angle is calculated and assigned to the nav_angles property of the Rover object.

#### 2. Autonomous mode
The simulator settings were set to 640x480, fastest, and windowed. The rover can navigate and map partially in the autonomous mode. One of the main problem is that when the rover comes to a fork, it begins to make circles without moving forward. The reason is calculating the angle by taking the mean of the angles to the navigable pixels.
Another problem is locating the rocks and picking them up is not implemented.


