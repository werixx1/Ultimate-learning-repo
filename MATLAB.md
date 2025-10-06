#### Functions for preparing data cheatsheet

1. Datastore = variable for storing multiple images
```matlab
imgs_datastore = imageDatastore(path_to_images, "IncludeSubfolders", true, 
"LabelSource", "foldernames") % use folder names as labels of classes
```

2. Displaying images from a datastore
```matlab
montage(imgs_datastore)
```

3. Imread(), imshow() - reading a single image file as variable and displaying it
```matlab
img = imread("example.jpg")
imshow(img)
% Using empty brackets as the second input will scale the display 
% based on the minimum and maximum values present in the image.
% imshow(im,[])
```

4. Extract image's first channel (make img gray)
```matlab
image(:,:,n) % n - channel value, 1 2 3
```
4. Using kernel with image (kernel as a matrix)
```matlab
filtered_image = conv2(kernel, image)
% ex kernel = [ 0 1 0, 1 -4 1, 0 1 0] - blur
imshow(filtered_image, [])
% for RGB image (all channels present)
filtered_image = imfilter(image, kernel)
```


3. Spliting data into train / test:
```matlab 
[train_df, test_ds] = splitEachLabel(imgs_datastore, proportion) % ex. 0.7 will 
% give 70/30 split
```
4. Data augmentation:
```matlab
augmented_ds = augmentedImageDatastore([size size], ds, augmentation_type)
```
5. Adjust learning options
```matlab
options = trainingOptions("algorithm_name", "InitialLearnRate", learn_value)
% ex. "adam" 0.0001
```

6. Return the number of non zero matrix elements (usefull when calculating accuracy)
```matlab
N = nnz(matrix)
% for accuracy
accuracy = nnz(test_data.Labels == predicted_labels) / length_of_data
```
7. Confusion matrix
```matlab
confusionchart(known_labels, predicted_labels)
```

5. Predicting values:
```matlab
minibatchpredict
```

Conv layer extract certain patterns (features), usually each conv layer in a bigger network has a different filter for detecting different things like ex. hertical edges, horizontal edges, whites etc