# Lane Detection

## Introduction

When approaching the problem of programming self driving cars, lane detection is a very immediate problem that one might encounter. Ensuring that the vehicle stays in the appropriate lane and responds to the twists and turns of the road is essential to creating a safe and functional self driving vehicle. In this project I will be outlining an image processing pipeline using the opencv library in python that can take images and videos as input and return the same images or videos with green lines fitted to the path of the immediate left and immediate right lane lines to the vehicle. 

## Pipeline

The pipeline for processing an image is about 7 steps and is outlined below:

1. Convert image to grayscale
2. Apply Gaussian blur to grayscale image
3. Apply Canny edge detection to the blurred image
4. Mask out region of image based on knowledge of camera position
5. Apply a Hough line transform to the masked out image
6. Fit a line to the left and right lane line segments
7. Add the fitted lines to the original image 

Here is the image we are starting with:

![Original](stage_1.png)

### Grayscale

The first step is to convert the image to grayscale. We convert the image to grayscale because we are not necessarily concerned with colors and working with a single channel image is less computationally expensive and less awkward than using a three channel image.

![Grayscale](stage_2.png)

### Gaussian Blur

Next we prepare the image for Canny edge detection by using a Gaussian blur. Since the edges in the image are detected by looking for a high rate of change, adding a blur reduces the noise in the image and creates better edge lines. If a blur is not applied there will be false edge detection due to the noise. When using the blur you can set the kernel size which is the size of the mask matrix that passes over the image and computes averages. A lower size kernel will pick up noise easily and create a lot of distinct edges and a higher size kernel will pick up noise less but create less distinct edges. 

![Gaussian Blur](stage_3.png)

### Canny Edge Detection

Canny edge detection takes a blurred image and an upper and lower threshold. Canny edge detection is processed similarly to the Gaussian blur kernel using what is called a Sobel kernel. The Sobel kernel approximates the intensity gradient in the horizontal and vertical directions. If it falls within the upper and lower threshold then it is recognized as an edge. 

![Canny Edge Detection](stage_4.png)

### Region Masking

The entire image should not concern us with the knowledge that the camera is in a fixed position on the vehicle. The part of the image we are actually concerned with is a trapezoid shape that starts at the bottom of the image near the left and right corners and ends near the horizontal center of the image and near the horizon line. We identify the approximate locations of the shape, create an image mask with the vertices of the shape, and use the bitwise_and function to apply the mask to the image which will black out everything not contained within the region defined by the supplied vertices.

![Region Mask](stage_5.png)

### Hough Line Transform

![Hough Line Transform](stage_6.png)

### Fitting Lines to Segments

![Fitting Lines to Segments](stage_7.png)

### Image Addition

![Image Addition](stage_8.png)


## Possible Improvements


## Conclusion
