# Tutorial 1: Creating the misty water effect

Date: Sept. 8th, 2022  

In this tutorial, we will create the misty water effect, a photography style that makes moving water (or any moving fluid/cloud) look soft and flowing. For example, let's compare an original image of the [Great Gorge](https://www.niagarafallstourism.com/play/outdoor-recreation/white-water-walk/) near [Niagara Falls](https://www.niagaraparks.com) with another image taken from the same location with the misty water effect applied:

![misty0](media/figure0.png)

The misty water effect can be created by taking a burst of (usually) 20+ images, and then doing a per pixel average.

### Organization

`README.md`: final product

`STUDENT.md`: student version, to be filled in

`data/`: contains burst of images we will be using for this tutorial

`media/`: example figures


## Learning objectives

1. Overview of OpenCV in Python (reading & writing)
2. Representing images as arrays
3. Grayscale vs. 3-channel colour images

## Topic 1: Overview of OpenCV in Python
To read/write an image, take a look at the [docs](https://docs.opencv.org/3.1.0/dc/d2e/tutorial_py_image_display.html).


Let's use OpenCV to read an example image of our scene in `data/` so we can see what we are working with:

![misty0](media/figure1.png)

The image above is a single capture from a burst of images. Even though the water is moving very fast,
the image still retains a lot of detail and does not have that smooth effect we want to create.

## Topic 2: Representing images as arrays

Now that we know how to read/write images with OpenCV, the next step is to investigate how our images are represented: arrays. Each coloured image can be considered as an NxMx3 NumPy array, where

-   N: number of rows of pixels in the image
-   M: number of cols of pixels in the image
-   3: number of colour channels, in this case it is RGB


The misty water effect can be generated with the following model:

>   Suppose we have $K$ images that we want to merge into one misty effect image. Let $I_k$ represent the $k$th image, where $k \in \{1, …, K\}$. The resulting misty image can be determined by a per pixel, per colour channel averaging:

>
>$$
>   I_{\text{misty}} = \frac{1}{K}\large\sum_{k=1}^{K}I_k
>$$
>

**Steps for creating a misty effect image**
1. Read in all images in `data/`. We need a lot of images to create the effect
2. Stack all images into a single array such that the stack has dimensions (K, N, M, 3). Take a look at these [NumPy docs](https://numpy.org/doc/stable/reference/generated/numpy.stack.html) for hints on doing the stacking.
3. Average over dimension 0 (K) to get the misty image of size (N,M,3). Take a look at these [NumPy docs](https://numpy.org/doc/stable/reference/generated/numpy.mean.html) for hints on doing the averaging


Following the steps above and applying it to all 20+ images in `data/`, the misty water effect image we get is:

![misty0](media/figure2.png)

Compared to the single capture from a burst of images in the [previous section](#topic-1-overview-of-opencv-in-python) the water looks much smoother, achieving the misty effect we wanted.

## Topic 3: Grayscale vs. 3-channel colour images

In the previous two sections, we chose to manipulate the coloured (RGB) image. We can also choose to read our images in greyscale:

![misty0](media/figure3.png)

Repeating the same exercise as before with generating the misty water effect on greyscale images:

![misty0](media/figure4.png)
