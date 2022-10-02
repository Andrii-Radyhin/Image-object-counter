# Internship-Description-Task-2

Abstract: This task needs more research on wide angles. But with our selection of the parameters, it works in our case. Below is my suggestion not to select parameters by hand.

We need a clear understanding of what is fully visible. I guess that for paving stone is exact what we can see, but for wall bricks there might be some cases:

1) Assume that it's the same as for paving stones.
2) Bricks have a wide and narrow side, but it's rotated in the corners and at the joints for a better connection, so we can see only the smaller side of the brick. Another solution would be to detect only bricks with visible wider sides and other as parts. I choosed this option.
3) 
Here are some images to understand geometrically:

![alt text](images/results.PNG)

For this image, it is the same situation: two bricks that can have parts inside a wall:

![alt text](images/results.PNG)

## Description of the algorithm

I will use opencv for this task, due to [cv2.findContours](https://docs.opencv.org/4.x/d3/dc0/group__imgproc__shape.html#gadf1ad6a0b82947fa1fe3c3d497f260e0)

First, we need to prepare our images. I will highlight borders using some filters.

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

We can use cv2.contourArea to calculate the average of all areas. I choosed the average area from ALL bricks because, on the corners and due to wide angles, there might be mistakes, but bricks that are fully visible can influence our average to make the area coefficient more believable.

In the first image, for example, if the bricks were squares and we wanted threshold by x-length by selecting a coefficient of 0.75 (x-length 0.75 avg), in areas, it would be 0.05625, so we can get a coefficient that fits by adding some value to 0.05625. So we need a threshold coefficient for each image, due to distortion.

## Results

Total bricks in the image: 54, Parts: 20, Full: 34

![alt text](images/results.PNG)

Total bricks in the image: 373, Parts: 106, Full: 267

![alt text](images/results.PNG)

Total bricks in the image: 84, Parts: 20, Full: 64

![alt text](images/results.PNG)

Total bricks in the image: 95, Parts: 25, Full: 70

![alt text](images/results.PNG)


## Solution report
At the end i want to suggest a solution to not select parameters by hands.
I would create a multiple regression model, that takes as input an image of the wall, and outputs
vector with parameters for canny, dilate or even area coefficient, then use this algorithms with a given parameters and perceive, as a predicition, number of bricks, for example. In this case, we must not forget to check continuity of the opencv operations, or use numerical gradient: (f(x+h) - f(x))/h.
