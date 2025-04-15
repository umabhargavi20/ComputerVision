# ComputerVision
Analog clock to Digital clock using Computer Vision

Abstract.The reason for converting analog time to digital time using image processing is to automate the extraction of time information from analog clock faces. This allows for integration with systems and applications reducing the reliance on manual time reading and enabling smooth interaction between analog and digital timekeeping methods. The method used includes preparing the image by detecting edges and applying the Hough Transform to locate the lines that represent the clock hands. We then group these lines based on their angles to differentiate between the hour and minute hands. By analyzing these lines our program can accurately convert analog clock time into format making the  process more automated and precise. As a result of this program, analog time is successfully converted into digital time using image processing, demonstrating that clock hands can be accurately detected and analyzed, resulting in a digital representation of the displayed time.


Introduction. The reason for automating the conversion of time to time through image processing is to make it easier to extract time related information from analog clocks for various purposes, such as smart home automation, data recording and improving accessibility for visually impaired individuals. In the field of computer vision and image processing current methods for detecting clock hands often rely on techniques such as contour tracing, skeletonization of the image, or machine learning models that are trained to recognize clocks.
This program follows an approach by using the Hough Transform for detecting lines and clustering them to identify hour and minute hands. While this is in line with methods the uniqueness may lie in the parameters chosen for line clustering and how these clusters are analyzed to determine the digital time. Also, the built-in cv2 Hough transformation function is not used here to prevent a trivial solution. The program demonstrates an implementation that bridges the gap between analog and digital timekeeping with applications, in IoT, robotics and assistive technologies.


Approach.
The program follows a step, by step process to tackle the task of converting analog time to time:

1. Image Loading and Preprocessing: The program begins by loading a grayscale image of an analog clock. Applies the Canny algorithm for edge detection, which helps highlight features.

2. Line Detection using Hough Transform: The Hough Transform technique is utilized to detect lines in the edge detected image. This step aims to identify the hour and minute hands of the clock.

3. Clustering of Detected Lines: The program groups the detected lines into clusters based on their angles using a threshold value that helps differentiate between hour and minute hands.

4. Generating Summaries: For each cluster a summary is generated by considering the angle and maximum length of the lines within that cluster. These summaries provide information for later time calculation.

5. Time Calculation: By analyzing the clusters, their angles and lengths used to calculate the 
representation of time in terms of hours and minutes.

Obstacles & Solutions:

1. Parameter Tuning: It is crucial to select parameters for edge detection Hough Transform and clustering techniques. To address this challenge we used an approach where parameters are adjusted based on inspection and empirical results. The size of the image also affects the parameter for areas such as the separation between pixels

2. Handling Disconnected Lines: If there are cases where lines are not continuous or disconnected then the program handles them by restarting the search for points whenever a disconnection is detected. This will allow the longest continuous line to be found and used along a specific hough coordinate.

Sorting the line clusters by angle is crucial, in determining the order of the hour and minute hands. This ensures that the clock time is interpreted accurately.

Design Choices:

Built-in functions: the built-in cv2 Canny function is used to get edges. This is because if the edge information is inaccurate at the beginning of the program, then the chances of getting incorrect data increases. We wanted to mainly avoid using the built-in Hough transformation program since it is the center of the system and we were able to accomplish this.

Line Clustering: The decision to group lines based on their angles allows the program to differentiate between the hour and minute hands taking advantage of the arrangement of clock hands.

Thresholding: A threshold is used to filter out lines that don't significantly contribute to the structure making it more robust against noise.

Visualization: Plotting the detected lines on the image helps in understanding decisions based on values related to the lines found. Makes it easier to debug.

Image Input: For our program, the images of the clock have to be at the center of the image. Most of the time spent was on the Hough transformation implementation and did not have time to make an additional feature of detecting a clock anywhere in an image

Code Attribution:

To sum up, this program demonstrates an approach to converting analog time to time. It tackles challenges through parameter tuning and algorithmic choices. The design decisions align well with clock faces characteristics. Although standard computer vision techniques have been used as inspiration, this implementation appears original and uses a less trivial method.

judgment calls you made in your approach.

Experiments and results. Provide details about your experimental arrangement. (For example, describe the datasets that you experimented with, number of images or videos, train/test split  if you used machine-learning algorithms, etc.) Describe the metrics that you used to evaluate how well your approach is working. Include clear figures and tables, as well as illustrative qualitative examples if appropriate. Be sure to include obvious baselines to see if your approach is doing better than a naive approach. (As an example, if you implemented a classifier, you might compare its accuracy with the accuracy of a classifier that made random decisions.) Also discuss any parameters of your algorithms, and tell us how you set the values of those parameters. If reasonable, show how the performance varies as you change those parameter values. Be sure to discuss any trends you see in your results, and explain why these trends make sense. Are the 

The first part to implement was the Hough transformation which is where we used the implicit representation to find lines. After getting the Hough coordinates that passed a specific threshold, we looked for the presence of the specific theta values that correspond to where the hands of the clock are pointing. Simultaneously, the coordinates of edges that correspond to the coordinate in the Hough space are stored. We would display the points found that passed the specified threshold and saw the lines detected. A lower threshold value would allow more Hough coordinates to pass, effectively allowing more points on the image to pass. Since different clock images have different sizes, we decided on a parameter that would be a fraction of a dimension of the image.



After this, the longest lines had to be filtered. This was done by iterating through each list for each Hough space coordinate and finding the longest consecutive lines. This would again take into account the size of the image when deciding how far apart pixels can be so they can be deemed as consecutive in a line. This would allow lines around the clock to be formed.


After getting the consecutive lines, we then had to get the lines that were closest to the center of the image. A simple distance formula was used to get the distance for each point in the line and if not one point was close, the line was removed. The lines closest to the center are what is shown in the output since they are all used for final calculation. These lines were then grouped together with their average angle and distance used to decide which hand of the clock they belonged to. These angles were put into formulas for calculating the minutes and hours of the clock. The grouping and calculation were from another project[1] that had the same topic and goal but different methods for getting lines.

With this,







<img width="370" alt="image" src="https://github.com/user-attachments/assets/f117c079-8c75-437f-b468-493d8bdb3a04" />


Qualitative results. Show several visual examples of inputs/outputs of your system (success cases and failures) that help us understand your approach.

Conclusion.In this report, we have discussed a Python program that employs image processing techniques, like edge detection and the Hough Transform to convert analog time into time. The method involves grouping detected lines based on their angles and summarizing these groups to determine the hours and minutes on a clock face. We tackled challenges such as fine tuning parameters and detecting consecutive pixels that form lines. Our design decisions primarily revolved around line clustering and thresholding. Despite conditions such as the clarity of the image, the program works and achieves the goal of the project.



References:

[1] Jinay Jain, "Telling the Time with Computer Vision," Dec 17, 2021.  [Online]. Available: https://blog.jinay.dev/posts/timekeeper/. [Accessed: Nov. 10, 2023].

[2] “Open Source Computer Vision, Hough Line Transform,” Nov 23, 2012. [Online]. Available: https://docs.opencv.org/3.4/d9/db0/tutorial_hough_lines.html. [Accessed: Nov. 12, 2023].






