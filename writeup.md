**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

The pipeline consists of 6 steps.
1. The input picture is converted to a grayscale picture
2. In order to extract structures a so called Canny image was created from the grayscale
3. a gaussian blure filter was applied
4. a region of interest was selected to only extract the lane lines relevant for the car
5. by trial and error, paramters for the Hough algorithm were figured and applied in order to extract line segments from the picture
6. an overlay image from the original color input picture and the lane lines picture was created and returned

Later on, in order to draw a single line on the left and right lanes, the draw_lines() was modified in several ways. Initially it was proceeded as suggested.
* the slopes were calculated on each line
* distinguished between positive and negative slope
* the mean slope was calculated
* given trigonometric functions the coordinates for each line was calculated
* the average line for each side was drawn with a thickness of 10

The results were noisy and not as expected. Afterwards the fitLine() function from OpenCV2 was applied. First in a way where an array of (x,y) coordinates was taken as input, later on each line, and then back where an outlier protection was applied. But then again the results and performance were dissappointing. So, despite all the effort, the first solution was picked.


###2. Identify potential shortcomings with your current pipeline

There are several shortcomings. First of all, the manual selection of _**Region of Interest**_ . Its a cool feature, but the pipeline should be able to do it by itself. Another problem is the noise. There is surely a sophisticated and elegant way where OpenCV or others have a nice function... The noise causes instabilities in the slopes and therefore the lines are constantly rotating (not as beatiful as the Udacity demo). Another issue might be, what if the lanes are red, yellow, or dirty. Surely the lines are going rotate even more. Moreover what if only one lane is available... Another problem might occure on stop lanes. Moreover what if cars occupies lanes (very common in some specific places in the world)


###3. Suggest possible improvements to your pipeline

There are many improvements to make. The question is how. Maybe there should be some constraints, that for example the camera is aligned in the center, and the horizon could be assumed at a specific level given a specific angle of the car (uphill/downhill)
Also processing of the lanes, using things like numpy and polyfit in order to create more robust lines could help somehow.