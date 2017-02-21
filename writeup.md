#**Finding Lane Lines on the Road** 

##Writeup - Ibrahim Almohandes

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:

* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image0]: ./test_images/solidWhiteCurve.jpg "Original"

[image1]: ./examples/gray.jpg "Grayscale"

[image2]: ./examples/edges.jpg "Canny Edges"

[image3]: ./examples/masked_edges.jpg "Masked Edges"

[image4]: ./examples/line_image.jpg "Hough Lines"

[image5]: ./test_images/out_solidWhiteCurve.jpg "Final"

---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of the following 5 major steps, for each input image:

1. convert the image to grayscale
2. apply Gaussian smoothing, then Canny Edge Detection on the grayscale image
3. create masked edges by filtering out the edges outside the region of interest
4. from the masked image, create Hough lines (in red) on a blank color image (of the same size)
5. create the output image by combining the Hough-lines image with the original image


In order to draw a single line on the left and right lanes, I modified the draw_lines() function by doing the following:

- First, I separated the line segments into two lists of points, one with negative slope and the other with positive slope, while filtering out noisy lines that are almost horizontal
- then, I applied linear regression (from `scikit-learn`) on the two point groups to create two fitted lines for drawing,
- then, from the resulting slopes and intercepts, I generated the start and end points of each line (given the horizontal boundaries of the region of interest, while filtering out the lines roughly outside the vertical boundaries)
- finally, I drew the two lines from the start and end points

Here, I am including intermediate results for one of the images to show how the pipeline works: 

![Original][image0]

![Grayscale][image1]

![Canny Edges][image2]

![Masked Edges][image3]

![Hough Lines][image4]

![Final][image5]

###2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the images have different dimensions. In this case, we need to dynamically identify the region of interest

Another shortcoming could be when the light visibility is not as clear as in the pictures


###3. Suggest possible improvements to your pipeline

A possible improvement would be to do curve fitting instead of fitting/averaging only straight lines (the optional challenge)

Another potential improvement could be to do color filtering to exclude line segments that are neither yellow nor white
