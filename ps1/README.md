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
the origin placed one pixel above and to the left of the upper-left pixel of the image  
and with the Y-axis pointing downwards