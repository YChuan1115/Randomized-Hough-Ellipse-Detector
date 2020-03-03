# Randomized-Hough-Ellipse-Detector

* Purpose: find an ellipse
* Date: 20190915

### prerequisite
```
cv2, numpy, matplotlib, skimage, pandas, random
```

Following the protocol of [Ellipse Detection Using Randomized HoughTransform](https://www.researchgate.net/publication/238703185_Ellipse_Detection_Using_Randomized_Hough_Transform)

### Canny edge detecor
* Noise reduction
* Gradient calculation
* Non-maximum suppression
* Double threshold

### Randomly pick three points
Use random.sample() to select three points; then, find the parameter of ellipse as a candidate by these points.  

### Determining Ellipse Center(p, q)
* Determine the equation of the line for each point where the line’s slope is the gradient at the point.
* Determine the intersection of the tangents passing throughpoint pairs (X1,X2) and (X2,X3).
* Calculate the bisector of the tangent intersection points. Thisis a line from the tangent’s intersection,t, to the midpoint of the twopoints,m.
* Find the bisectors intersection to give the ellipse’s center,O

### Determining semimajor (a) and semiminor axis’ (b) )
* Shift the ellipse to origin. (Shift center (p, q) to (0, 0))
* Solve ellipse equation with the three points  

![](/image/findinghough.png)  

### Verifying the Ellipse Exists in the Image
* The sign of 4AC−B^2 determines the type of conic section:
1. positive --> Ellipse or Circle
2. zero --> Parabola
3. negative --> Hyperbola
* ellipse out of image

### Constraint
* semi major axis bound
* semi minor axis bound
* flattening bound (customized)
* nucleus-cell ratio bound (customized)

### Accumulating
* weighted average
* select the best result
* plot the best result by matlibplot


# Comparison with the original Hough ellipse transform

### skimage.transform hough_ellipse

n = 337, time = 2.67 sec  
n = 439, time = 5.1 sec  
n = 644, time = 15.3 sec  
time complexity: more than quadratic. (impracticable)

![](/image/hough.png)



### randomized hough ellipse detector

the number of iteration for randomly picking pixels = edge pixels * 10  
time complexity: linear  

n = 337, time = 0.7 sec  
n = 439, time = 1.1 sec  
n = 644, time = 1.5 sec  
Nice!

![](/image/Rhough.png)




