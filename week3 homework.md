___

## Colab 1

**QUESTION 1: What do you notice regarding the effect of changing the threshold? State both your observations and the reasons for the observations. Show your code, results and answer in the report.**

ANSWER: I notice that increasing the threshold makes the edge detection pick up on less noise. This could be because increasing the threshold value increases gradient magnitude at which we decide a pixel is part of an edge, effectively picking up on less noise and more likely capturing actual edges. The code can be found below.

```python
# Complete Task 1 here

# magnitude = sqrt(shakey_sobel_x**2 + shakey_sobel_y**2)

def magnitude(x,y):
    return np.sqrt(x**2+y**2)
m=magnitude(shakey_sobel_x,shakey_sobel_y)
print(np.average(m))
print("no thresholding")
show_rgb_image(m)
print("m>20")
show_rgb_image(m>20)
print("m>40")
show_rgb_image(m>40)
print("m>60")
show_rgb_image(m>60)

```

Results in order of declaration in the code LTR
![[image.png]]

___ 

**QUESTION 2: What do you notice regarding the difference between Sobel and Roberts? State both your observations and the reasons for the observations.**

ANSWER: I noticed that the Roberts kernel requires a lower thresholding value to achieve similar edge detection. This could be because Roberts kernel is a smaller 2 by 2 kernel which makes it more sensitive to gradient fluctuations than Sobel's kernel is.

___
**QUESTION 3: What do you notice regarding the difference between magnitude and absolute when calculating the edge? State both your observations and the reasons for the observations.****

ANSWER: I notice that the approximation is just as good as the original calculation across several thresholds. This could be because mathematically, when we reach an edge, the difference between $G_x$ and $G_y$ becomes very large and one of them can be ignored, leading to the magnitude being close to either $\sqrt{G_x^2} = |G_x|$ or $\sqrt{G_y^2} = |G_y|$ in the actual case and the same being true in the approximated case. Therefore when it comes to edge detection, the sum of absolute values is a close enough approximation to actually computing the gradient magnitude (which can be a computationally expensive operation to perform repeatedly)        

___


## Colab 2

**Question 1:** Using the built-in procedure ```scipy.signal.convolve2d``` convolve the image with the 3x3 Gaussian filter, and then the 5x5 filter. Can you see any difference between them? Try applying an edge filter to each and thresholding. Refer to the previous assignment to understand the convolve2d function. Can you describe the effect in comparison with applying the edge filter to the image directly?

**Answer 1:**

The 5x5 filter makes the image look slightly blurrier although the difference is not visually striking. 

   ![[Pasted image 20250216202937.png|481x321]]  
   
Applying the Sobel filter to the 3x3 gaussian filtered Shakey image without thresholding yielded a good edge map. Applying thresholding around the mean of the magnitude yielded a good edge map as well but the threshold values are much smaller than the non-gaussian filtered image (the average gradient magnitude is roughly 300x smaller). A similar case can be observed with 5x5 gaussian filter and thresholding around the mean gradient magnitude. The differences between the edge maps generated using the Sobel filter on the 3x3 gaussian filtered image and the 5x5 gaussian image are not visually discernable. Although the mean gradient magnitude of the 5x5 gaussian image was about 1.22 times smaller than that of the 3x3 gaussian filtered image. To answer the last question, the difference between applying the edge filter after gaussian filtering and applying the edge filter directly on the image lies mainly in the gradient magnitude, which is highly suppressed in the former due to gaussian filtering smoothing out the image.

___
**Question 2:**

**What happens to the image as you increase the size of the mask? What happens as you increase the size of `std_dev`? What happens to the edges in the heavily blurred case? What  is  the  effect  of  increasing  the  size  of  the  Gaussian  Filter  (3x3  versus  5x5  for  example)?What is the effect of changing the standard deviation s? Why do you see what you see?**

**Answer 2:**

Increasing the size of the mask makes the image appear blurrier (and also increase the size of the bezels ?? (cant explain why))

![[image-1.png]]

Increasing the standard deviation makes the images appear noticeably blurrier. In the heavily blurred case ($\sigma$=10, $\mu$=0), the edge detection is quite poor.

Below are the images with $\sigma$=2, $\mu$=0 and $\sigma$=10, $\mu$=0 and the Sobel x and y filters applied to them.

![[image-2.png]]

Explanation: Edge detection relies strongly on difference in gradient magnitudes. This difference is smoothed out as the standard deviation increases, or gaussian filters are applied, leading to unclear edges when edge filters are convolved with the image.


Question 3

still thinking through it hehe

