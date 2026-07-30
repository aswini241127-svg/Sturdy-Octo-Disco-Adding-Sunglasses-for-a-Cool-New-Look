
# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look

 Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

# Features:

1.Detects the face in an image.


2.Places a stylish sunglass overlay perfectly on the face.


3.Works seamlessly with individual passport-size photos.


4.Customizable for different sunglasses styles or photo types.

# Technologies Used:
1.Python

2.OpenCV for image processing


3.Numpy for array manipulations

# How to Use:
1. Clone this repository.

2.Add your passport-sized photo to the images folder.


3.Run the script to see your "cool" transformation!


# Applications:
1.Learning basic image processing techniques.


2.Adding flair to your photos for fun.


3.Practicing computer vision workflows.


Feel free to fork, contribute, or customize this project for your creative needs!
# PROGRAM:
Developed by: ASWINI D Register Number: 212225240015
```
# Import libraries
import cv2
import numpy as np
import matplotlib.pyplot as plt
# Load the Face Image
faceImage = cv2.imread('pic1.jpeg')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
```
<img width="500" height="555" alt="image" src="https://github.com/user-attachments/assets/0daac359-37ab-417a-9298-41975c593e93" />

















```
faceImage.shape
glassPNG = cv2.imread('sun (2).png',-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")
```
<img width="778" height="356" alt="image" src="https://github.com/user-attachments/assets/7f9ee178-ebd2-44d5-bcff-a544eb288b8d" />
















```
glassPNG = cv2.resize(glassPNG,(190,50))
print("image Dimension ={}".format(glassPNG.shape))
# Display the images for clarity
plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');
```
<img width="1378" height="242" alt="image" src="https://github.com/user-attachments/assets/39b802e4-b485-4f9b-bbc9-de7cbb3bbee6" />
























```
# Make a copy
#faceWithGlassesNaive = resized_faceImage.copy()
faceWithGlassesNaive = faceImage.copy()

# Replace the eye region with the sunglass image
faceWithGlassesNaive[150:200,160:350]=glassBGR

plt.imshow(faceWithGlassesNaive[...,::-1])

```
<img width="502" height="540" alt="image" src="https://github.com/user-attachments/assets/f5aefdfc-1eef-4620-a4b7-b3fa233adaae" />



















```

# Make the dimensions of the mask same as the input image.
# Since Face Image is a 3-channel image, we create a 3 channel image for the mask
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))

# Make the values [0,1] since we are using arithmetic operations
glassMask = np.uint8(glassMask/255)

# Make a copy
faceWithGlassesArithmetic = faceImage.copy()

# Get the eye region from the face image
eyeROI= faceWithGlassesArithmetic[150:200,160:350]

# Use the mask to create the masked eye region
maskedEye = cv2.multiply(eyeROI,(1-  glassMask ))

# Use the mask to create the masked sunglass region
maskedGlass = cv2.multiply(glassBGR,glassMask)

# Combine the Sunglass in the Eye Region to get the augmented image
eyeRoiFinal = cv2.add(maskedEye, maskedGlass)
`
# Display the intermediate results
plt.figure(figsize=[20,20])
plt.subplot(131);plt.imshow(maskedEye[...,::-1]);plt.title("Masked Eye Region")
plt.subplot(132);plt.imshow(maskedGlass[...,::-1]);plt.title("Masked Sunglass Region")
plt.subplot(133);plt.imshow(eyeRoiFinal[...,::-1]);plt.title("Augmented Eye and Sunglass")
```
<img width="1385" height="209" alt="image" src="https://github.com/user-attachments/assets/9a326b26-d29f-45b9-9ddd-eb57bf88b80b" />

































```
# Replace the eye ROI with the output from the previous section
faceWithGlassesArithmetic[150:200,160:350]=eyeRoiFinal
```









```
# Display the final result
plt.figure(figsize=[20,20]);
plt.subplot(121);plt.imshow(faceImage[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(faceWithGlassesArithmetic[:,:,::-1]);plt.title("With Sunglasses");
```
<img width="1405" height="777" alt="image" src="https://github.com/user-attachments/assets/94824837-c84e-4809-8572-5cbf6873b774" />



# Result:
The sunglasses PNG image was successfully superimposed onto the face image using alpha masking and image blending techniques in OpenCV. The final output shows a realistic face image with sunglasses correctly placed over the eyes.
