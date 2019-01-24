
# Project 1 - Finding lanes

Following the given goals and requirements for this project, below is a overview of how the solution works.

# Reflections

## Description
The pipeline consists on six steps as described below:

- **Choice menu**: Gives the user the choice of either testing the images or videos. These have to be inside their respective folders and these folder have to be inside the same working directory.
- **Reading image**: The original image/frame is read by using opencv's **cv2.imread()** method.
- **Converting to grayscale**: Converting to image/frame to grayscale by using opencv's **cv2.cvtColor()** method.
- **Blurring the image**: Applies a Gaussian blur to the image/frame, it also makes use of the opencv's **cv2.GaussianBlur()** method.
- **Finding edges**: finds edges within the image/frame. Opencv's **cv2.Canny()** method is used to extract these features.
- **Region of Interest**: Creates a mask with only the region of interest within the image/frame, saving machine resources and eliminating the risk to calculating over non-lanes edges detected on the image.
- **Finding lines**: Finds lines withing the previously calculated region of interest using opencv's  **cv2.cv2.HoughLinesP()** method. This probabilistc method is considerably faster than the original houghlines. To calculate the slope and intersect of these newly found lines, opencv's **np.polyfit()** method is apply to make the process of deciding the left and right lanes easier. The newly found lines with the previous step are now averaged so that the outcome is one smoother line which is then transformed to cartesean space. 
- **Combining the results**: These lines are then placed on top of the original image/frame to be displayed to the user.

The output of each step is saved in a directory:

- [1 - Choice_menu](1_Choice_menu)
- [2 - Original_image](2_Original_image)
- [3 - Converting_to_grayscale](3_Converting_to_grayscale)
- [4 - Blurring_the_image](4_Blurring_the_image)
- [5 - Finding_edges](5_Finding_edges)
- [6 - Region_of_interest](6_Region_of_interest)
- [7 - Finding_lines](7_Finding_lines)
- [8 - Combining_the_results](8_Combining_the_results)

## Potential shortcomings/suggestions

- At times the line is not as perfect as I would like, so a way to weed out lines we don't want should be found.
- The aesthetics of the outcome should be improved so that it becomes more professional looking.

