
# Project 1 - Finding lanes

Following the given goals and requirements for this project, below is a overview of how the solution works.

# Reflections

## Description
The pipeline consists on nine steps as described below:

- **Choice menu**: Gives the user the choice of either testing the images or videos. These have to be inside their respective folders and these folder have to be inside the same working directory.
- **Converting to grayscale**: Converting to image/frame to grayscale by using opencv's **cv2.cvtColor** method.
- **Blurring the image**: Applies a Gaussian blur to the image/frame, it also makes use of the opencv's **cv2.GaussianBlur** method.
- **Finding edges**: finds edges within the image/frame. Opencv's **cv2.Canny** method is used to extract these features.
- **Region of Interest**: Creates a mask with only the region of interest within the image/frame, saving machine resources and eliminating the risk to calculating over non-lanes edges detected on the image.
- **Finding lines**: Finds lines withing the previously calculated region of interest using opencv's  **cv2.cv2.HoughLinesP** method. This probabilistc method is considerably faster than the original houghlines. To calculate the slope and intersect of these newly found lines, opencv's **np.polyfit** method is apply to make the process of deciding the left and right lanes easier.
- **Averaging results**: The newly found lines with the previous step are now averaged so that the outcome is smoother.
- **Cartesean convertion**: The newly found lines with the previous step are transformed to cartesean space.
- **Combining the results**: These lines are then placed on top of the original image/frame to be displayed to the user.

The output of each step is saved in a directory:

- [test_images_gray](test_images_gray)
- [test_images_blur](test_images_blur)
- [test_images_canny](test_images_canny)
- [test_images_region](test_images_region)
- [test_images_hough](test_images_hough)
- [test_images_merged](test_images_merged)

To average and interpolate the lines on the **draw_lines** function, I try to find the lines going on the left and right side of the image. Each point of those sides were accumulated and first degree polynomial was fit to those points using **numpy.polyfit**. When the line equation was found, it was evaluated on the region of interest to define the points where the line would be shown on the image.

## Potential shortcomings/suggestions

- The lines shake a lot on the videos, a better way to average them should be possible.
- The line size should be improved.
- Bright points outside the lines were taking into account.

My pipeline starts off by giving the user the option of going through the images or videos. These images and videos should be in their respective folders inside the directory where the program is running from. After this option is made, the pipeline then converts the image, or frame to grayscale, then the image is blurred, despite knowing that the canny algorithm also applies blurring within its algorithm, then canny is applied to this frame/image. The image/frame has now been prepped to apply a region of interest by creating a mask with same size and shape as the original frame/image, but only displaying a prefined section of the image.

After that, houghlineP from the opencv library is applied and converted to cartesean space to be displayed onto the very same original frame. For displaying it onto the original frame, we dimmed the original frame/image down a bit so that the newly calculated lines show up better for the user.

Here are some pictures to show how the pipeline transcribes what I described above:
