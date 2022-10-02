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
