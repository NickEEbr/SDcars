
# Finding Lane Lines on the Road

The goals/steps of this project are the following:

- Make a pipeline that finds lane lines on the road.
- Reflect on your work in a written report.

# Reflections

## Description
The pipeline consists on six steps represented by six different functions:

- **Converting to grayscale**: Returns a gray scaled version of the input image using **cv2.cvtColor** method.
- **Blurring the image**: Applies a Gaussian blur to the provided image using **cv2.GaussianBlur** method.
- **Finding edges**: Use a [Canny transformation](https://en.wikipedia.org/wiki/Canny_edge_detector) to find edges on the image using **cv2.Canny** method.
- **Region of Interest**: Eliminate parts of the image that are not interesting in regards to the line detection (for now...).
- **Finding lines**: Use a [Hough transformation](https://en.wikipedia.org/wiki/Hough_transform) to find the lines on the masked image using **cv2.cv2.HoughLinesP**. It also adjust a line to the set of lines returned by the Hough transformation in order to have a clearer-two-lines representation of the road lines using **np.polyfit** method.
- **Combining the results**: Merges the output of **houghAction** with the original image to represent the lines on it.

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
