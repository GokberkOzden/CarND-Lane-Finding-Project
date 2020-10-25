# Project 1: Finding Lane Lines



---

Main purpose of the project is to create a pipeline to detect lane lines from an image or video input. Developed pipeline will be tested on different images and videos.



### 1. Pipeline

Created Lane Finding pipeline has twelve algorithm steps.
1.Get image size
   In this step, height and width information of the input frame is taken. 
2.Define region of interest
    Region of interest is defined as a triangular from bottom of the image to the middle.
3.Gray scale the image
    RGB image is transformed to a gray scaled image in this step.
4.Canny Edge Detection
    Canny Edge Detection is applied to gray scaled image with thresholds selected as 70-150.
5.Crop the image
    Take only the interested area of the image to detect lines.
6.Hough Transform
    Apply Hough transform to region of interest to detect lines.
7.Draw Lines
    In this step, found lane lines are ready to be drawn on original image. It is possible to draw a contionus line on top of seperated lanes by playing with Hough transform parameters. However, it will not give a robust result, espically in video input. Therefore, in next steps a polynomial will be fitted on top of found lanes.
8.Seperate Right and Left Lanes
    Two lane lines are on right and left side of the image. They can be seperated by their slope values. So as a first step of polynomial fitting, found lines in Hough transfrom must be seperated.
    
9.Fit a polynomial for right and left lines.
    Two first order polynomials will be fitted to found right and left lines.

10.Define start and end points on y-axis for lines
    The polynomial needs a start and an end points. Previously, region of interest was defined from bottom to middle of the image as a triangular area. Hence, when considered on  y-axis lines shall be drawn from bottom to somewhere near to middle of the image. The exact point is arbitrary as long as it is in the region of interest. 

11.Calculate start and points on x-axis
    Put the found y-axis values on the polynomial, it will result the x-axis values.
    
12.Draw lines on top of the original image
    To draw lines on top of the original image. First create a blank image and then loop over the image to draw lines. Once you have the image only consist od the lines, you can merge it with the original.





### 2. Identify potential shortcomings with your current pipeline


One shortcoming of the implementation is using a one dimensional polynomial for lines. When the lane lines have curves, the polynomial will not fit and lane finding will be impossible during the cornering.


### 3. Suggest possible improvements to your pipeline

For the solution of the possible shortcoming, a 2D polynomial could be fitted as lines or instead of using the polynomial as line, only near bottom of the frame, polynomial can be used. When tempered with the Hough transform parameters, seperated lane lines can be drawn as a contionus line. Only problem occurs in the video when the empty space between lane lines gets to the bottom of the image. Therefore more straight lines will be fitted with 1D polynomial and Hough Transform can create the curved lines.  
