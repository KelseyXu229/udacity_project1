# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/solidWhiteCurve.jpg 

[image2]: ./newpipeline/challenge_color_select.jpg 

[image3]: ./newpipeline/challenge_color_select_line.jpg 

[image4]: ./newpipeline/challenge_right_select_line.jpg

[image5]: ./newpipeline/challenge.jpg

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.


My first pipeline is similar to the courses of udacity,consisted of 6 steps.First,I converted the images to grayscale,then I also include 

Gaussian smoothing,and then applyed Canny to the image blur_gray,and then masked out a polygon region of interest, and then uesd Hough 

transform to detect line segments,finally drawed lane lines with these line segments and combined lines image with oringal image, the result 

of first test which called "Build a Lane Finding Pipeline"  as shown below:

![alt text][image1]

My first pipeline is verified to be effective for the other tests except the Optional Challenge.In order to up for the challenge,I modified my 

first pipeline.The final pipeline integrates the new method called color_select with the old method of first pipeline,and the left lane line 

is only processed by color_select method, and the right lane line is only processed by old method. 

(So why should i have to add the color_select method? Because in the challenge.mp4, left lane line is yellow and there is a relection of some brantches on it, if i used my first pipeline to process, the result of the left lane line must be very terrible.)


First,in order to draw first left lane line only,I converted the images to HSV,and used cv2.inrange() function to select yellow objects.

![alt text][image2]


Then also followed 6 steps of the my first pipeline,finally aquired the left lane line only.

![alt text][image3]

Second,in order to draw another right lane line only,I directly used the 6 steps of the my first pipeline,except the parameters of vertices.I 

changed the parameters of vertices to make the polygon focus on right lane line accurately. 

![alt text][image4]

Finally,I combined the left lane line and right lane line with original image:

![alt text][image5]


At last,let me explain the modified the draw_lines() function.In order to draw the full length of the visible lane based on the line segments 

identified with the Hough Transform, the draw_lines() function modified by referenced to advises.First,line segments are classified by sign of 

slope as positive lines or negative lines, and these positive lines or negative lines were filtered by own scope.And then filtered positive 

lines or negative lines are process seperately,but the method is the same.I used iteration of the slopes and biases to generate the slope and 

bias to define the visible lane line. The iteration fomulas are,

current_slope=current_slope*0.6+new_slope*0.4, 

current_bias=current_bias*0.55+new_slope*0.45.



### 2. Identify potential shortcomings with your current pipeline


In spite of my current pipeline roughly meeting the requirements of all videos,but One potential shortcoming would be that,there are some 

moments the drawed lane lines disappeared,or have a little deviation. 

Another shortcoming could be my code is verbosity.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to the parameters should be tweaked to make the results more effective. and 

Another potential improvement could be the color select method should be designed able to select yellow and white objects simultaneously,so as 

to the methods will be smarter and concise.
