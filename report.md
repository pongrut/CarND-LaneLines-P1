# **Finding Lane Lines on the Road** 

Pongrut Palarpong  
Febuary 20, 2018

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 9 steps. First, I enhanced the images by fading its color and increasing contrast to make algorithm is more robust on different lighting conditions, then I followed standard step 2 to step 8, and the final step I added draw_poly to fill color on road space to generate clear visibility.

#### Pipeline Steps Summary.
1. image_enhance: Enhances images by using PIL.ImageEnhance to modify color and contrast.
2. color_selection: Filters images by colors within the specified boundaries.
3. region_of_interest: Only keeps the region of the image defined by the polygon formed from `vertices`.
4. grayscale: Applies the Grayscale transform, this will return an image with only one color channel
5. gaussian_blur: Applies a Gaussian Noise kernel to blur images.
6. canny: Uses Canny Edge detection to detect edges.
7. hough_lines: Uses edge detection output image to perform hough transform to get lines from parameter space.
8. draw_lines: Finds the left and right representative lines.
9. draw_poly: Fills color into road space.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by calling best_2_lines() to get left and right line. The best_2_lines() function take 2 arguments first image itself and lines from hough_lines function, all potential horizontal lines are filter out and the rest are separate into to group. The right lines are line that has positive slope (slope greater than zero) and another group are left lines, then create representative lines of each group by using a one dimensional polynomial to find x1, x2 with define y_min (y right under middle of the image) and y_max (height of the image).

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![proposed best fit lines][best_fit_lines_demo.jpg]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 
- Lighting condition e.g. brightness, contrast, lighting color
- Sharp bend
- Crossroads
- Bike Lane

Another shortcoming could be ... 


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
