# Problem Set 1: Edges and Lines

## Description
This problem set is your first “vision” project where you compute an “answer” – that is some structural or   
semantic description as to what is in an image. You’ll find edges and objects.  
And you’ll learn that some methods work well for carefully controlled situations and hardly at all when you relax those constraints.

## Questions
### 1. Store Edge Image
For this question we will use input/ps1-input0.png. 
This is a test image for which the answer should be clear, where the “object” boundaries are only lines. 

    a) Load the input grayscale image (input/ps1-input0.png) as img and generate an edge image – which is a   
    binary image with white pixels (1) on the edges and black pixels (0) elsewhere.   
    Use one operator of your choosing – for this image it probably won’t matter much.   
    If your edge operator uses parameters (like ‘canny’) play with those until you get the edges you would expect to see.

    Output: Store edge image (img_edges) as ps1-1-a-1.png

### 2. Implementing Hough Transform
Implement a Hough Transform method for finding lines. Note that the coordinate system used is as pictured below with   
the origin placed one pixel above and to the left of the upper-left pixel of the image and with the Y-axis pointing downwards.

Thus, the pixel at img(r,c) corresponds to the (x,y) coordinates (r,c), i.e. x=c and y=r.   
This pixel should vote for line parameters (ρ,θ) where: ρ = x⋅cos(θ) + y⋅sin(θ), and θ = atan2(y,x).

This has the effect of making the positive angular direction clockwise instead of counter-clockwise in  
the usual convention. Theta (θ) = zero still points in the direction of the positive X-axis.

    a) Write a function hough_lines_acc that computes the Hough Transform for lines and produces an accumulator array. Your code should conform to the specifications of the Matlab function hough: http://www.mathworks.com/help/images/ref/hough.html
    Note that it has two optional parameters RhoResolution and Theta, and returns three values - the hough accumulator array H, theta (θ) values that correspond to columns of H and rho (ρ) values that correspond to rows of H.

    Apply it to the edge image (img_edges) from question 1:
            [H, theta, rho] = hough_lines_acc(img_edges);
    Or, with one optional parameter specified (θ = integers -90 to 89, i.e. 180 values including 0):
            [H, theta, rho] = hough_lines_acc(img_edges, 'Theta', -90:89);

    Function file: hough_lines_acc.m containing function hough_lines_acc (identical name)
    Output: Store the hough accumulator array (H) as ps1-2-a-1.png (note: write a normalized uint8 version of the array so that the minimum value is mapped to 0 and maximum to 255).

    b) Write a function hough_peaks that finds indices of the accumulator array (here line parameters) that correspond to local maxima. Your code should conform to the specifications of the Matlab function houghpeaks:
    http://www.mathworks.com/help/images/ref/houghpeaks.html
    Note that you need to return a Qx2 matrix with row indices (here rho) in column 1, and column indices (here theta) in column 2. (This could be used for other peak finding purposes as well.)
    
    Call your function with the accumulator from the step above to find up to 10 strongest lines:
            peaks = hough_peaks(H, 10);
    
    Function file: hough_peaks.m
    Output: ps1-2-b-1.png - like above, with peaks highlighted (you can use drawing functions).
    
    c) Write a function hough_lines_draw to draw color lines that correspond to peaks found in the accumulator array. This means you need to look up rho, theta values using the peak indices, and then convert them (back) to line parameters in cartesian coordinates (you can then use regular line-drawing functions).
    
    Use this to draw lines on the original grayscale (not edge) image. The lines should extend to the edges of the image (aka infinite lines):
            hough_lines_draw(img, 'ps1-2-c-1.png', peaks, rho, theta);
    
    Function file: hough_lines_draw.m
    Output: ps1-2-c-1.png - can be saved as a plot directly from hough_lines_draw().
    It should look something like this:
    
    
    You might get lines at the boundary of the image too depending upon the edge operator you selected (but those really shouldn’t be there).
    
    d) What parameters did you use for finding lines in this image?
    Output: Text response describing your accumulator bin sizes, threshold and neighborhood size parameters for finding peaks, and why/how you picked those.

### 3. Add some noise
    a) Use ps1-input0-noise.png - same image as before, but with noise. Compute a modestly smoothed version of this image by using a Gaussian filter. Make σ at least a few pixels big.
    Output: Smoothed image: ps1-3-a-1.png

    b) Using an edge operator of your choosing, create a binary edge image for both the original image (ps1-input0-noise.png) and the smoothed version above.
    Output: Two edge images: ps1-3-b-1.png (from original), ps1-3-b-2.png (from smoothed)
    
    c) Now apply your Hough method to the smoothed version of the edge image. Your goal is to adjust the filtering, edge finding, and Hough algorithms to find the lines as best you can in this test case.
    Output:
        - Hough accumulator array image with peaks highlighted: ps1-3-c-1.png 
        - Intensity image (original one with the noise) with lines drawn on them: ps1-3-c-2.png
        - Text response: Describe what you had to do to get the best result you could.