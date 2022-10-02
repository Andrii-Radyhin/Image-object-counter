# Internship-Description-Task-2

Abstract: This task need more research for wide angle. But with selection of the parameters it works in our case. Below is my suggestion not to select parameters by hands.

We need clear understanding what is fully visible parts. I guess that for paving stone is exact what we can see, but for wall bricks there might be some cases:

1) Assume that it's the same as for paving stones.
2) Bricks have a wide and narrow side, but it's rotated in the corners and at the joints for a better connection, so we can see only smaller side of the brick. If we want to detect only bricks with visible wider side and other as parts there would be another solution. I choosed this option.

Here is some images to understand geometrically:

![alt text](images/results.PNG)

For this image is the same situation, two bricks that can have parts inside wall:

![alt text](images/results.PNG)

## Description of the algorithm

I will use opencv for this task, due to [cv2.findContours](https://docs.opencv.org/4.x/d3/dc0/group__imgproc__shape.html#gadf1ad6a0b82947fa1fe3c3d497f260e0)

First we need to prepare our images. I will highlight borders with some filters.

1) Convert image into grayscale image.

![alt text](images/results.PNG)

2) Edge detection is required for counting, but first, using GaussianBlur, the image must be blurred to remove noise.

![alt text](images/results.PNG)

3) Now we will detect edges using a canny algorithm

![alt text](images/results.PNG)

4) To make more thicker and visible the edges --> cv2.dilate


![alt text](images/results.PNG)

5) And last, use cv2.findContours with algorithms such as: cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_NONE. (Here is also fit cv2.CHAIN_APPROX_SIMPLE) 

![alt text](images/results.PNG)

### Using area to understand which brick is a part:

We can calculate with cv2.contourArea and then take average from all areas. I choosed average area from ALL bricks because on the corners and due to wide angles
there might be mistakes, but bricks that are fully visible can influence on our average to make coefficient more believable and of course we need a trashhold coeffcient.

