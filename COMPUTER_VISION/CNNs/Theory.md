<h3 align="center">Theory</h3>

  <p align="center">
    Theory and concepts behind CNNs
    <br>
    <a href="">Resources</a>
    ·
    <a href="">Main</a>
  </p>
</p>


## Table of contents

- [Basic understanding](#basic-understanding)
    - [Convolution](#convolution)
    - [Stride](#stride)
    - [Pooling](#pooling)
    - [Padding](#padding)
    - [Normalization](#normalization)


## Basic understanding
> Most common notions in CNNs

### Convolution
**Definition**
<br>
Procedure when you slide **kernel** (a small matrix) on image to extract it's characteristic features (resulting matrix is called **feature map**), to get feature map values you multiply overlapping values at each position 
Visualisation    |  Example 
:-------------------------:|:-------------------------:
![convolution](/resources/imgs/CV_1.gif) |  ![conv_math](/resources/imgs/CV_3.png)

| Math formula |
| -------- |
|![math_convolution](/resources/imgs/CV_8.png) |  ![example](/resources/imgs/CV_9.png) |
| ![example](/resources/imgs/CV_9.png) |


<!-- ![conv_func](../imgs/CV_7.png) -->
### Stride 
**Definition**
<br>
**Number** of pixels by which we **move** the filter across the input image (right and down)
![stride_example](/resources/imgs/CV_5.png)

### Pooling 
**Definition**
<br>
Technique to **reduce** spatial dimensions **(width and height)** of feature map, it works by sliding a two-dimensional (2x2 window) filter over each channel of a feature map and **summarizing** the features within the region covered by the filter 
<br>
`Simply put: taking the **maximum** value of the four numbers in the window`
<!-- reshape this to be smaller pls -->
![pooling](/resources/imgs/CV_2.png)

### Padding
**Definition**
<br>
Adding several **rows** or **columns** to the image (usually values there are set to 0), it is used to prevent feature map being too small during feature extraction (it becomes smaller after every kernel sliding), 
    - `it's used to prevent data loss at edges`, 
    - setting padding to true will make feature map the same size as original image (?)

![alt text](/resources/imgs/CV_4.webp)

### Normalization
**Definition**
<br>
Normalization **scales pixel values** to a consistent range, most commonly **[0, 1]** or **[-1, 1]**. This improves model convergence, helps gradients behave, and often results in better accuracy.
- prevents one feature (pixel intensity) from dominating others
- reduces training time
- makes models numerically stable


**Summary**:
![summary](/resources/imgs/CV_6.png)


