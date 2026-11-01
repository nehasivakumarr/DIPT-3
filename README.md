# Histogram Equalization Using OpenCV (Grayscale & Color Images)
## Aim
To write a Python program using OpenCV to perform histogram equalization on both grayscale and color images to enhance image contrast and brightness.

The program performs the following operations:

- Read and display a grayscale image
- Plot histogram of the grayscale image
- Apply histogram equalization on grayscale image
- Read and display a color image
- Plot histogram of B, G, R channels
- Convert image to HSV color space
- Apply histogram equalization on the Value (V) channel
- Convert the enhanced image back to BGR format
- Display original and enhanced images with histograms
---
## Software Used
- Anaconda – Python 3.7
- Jupyter Notebook / VS Code
- OpenCV (cv2)
- NumPy
- Matplotlib
---
## Algorithm

### Step 1:
Import the required libraries: OpenCV, NumPy, and Matplotlib.

### Step 2:
Read the image parrot.jpg in grayscale format.

### Step 3:
Display the grayscale image and plot its histogram.

### Step 4:
Apply histogram equalization using cv2.equalizeHist() to enhance contrast.

### Step 5:
Display original grayscale image, its histogram, enhanced image, and its histogram using a 2 × 2 grid.

### Step 6:
Read the same image in color format.

### Step 7:
Split the image into B, G, R channels and plot their histograms.

### Step 8:
Convert the image from BGR to HSV color space.

### Step 9:
Apply histogram equalization on the V (Value) channel.

### Step 10:
Merge the channels and convert the image back to BGR format.

### Step 11:
Display original color image, histogram, enhanced image, and enhanced histogram using a 2 × 2 grid.

---
## Program 
### Developed By:
### Name: NEHA S
### Register No: 212225100030
```
import cv2
import numpy as np
import matplotlib.pyplot as plt
```
```
gray_img = cv2.imread('/content/marvelous picture of spiderman.jpg', cv2.IMREAD_GRAYSCALE)

if gray_img is None:
    print("parrot.jpg not found. Creating a dummy image for demonstration.")
    dummy_img = np.zeros((100, 100), dtype=np.uint8)
    for i in range(100):
        dummy_img[i, :] = i * 2.55  # Create a gradient from 0 to 255
    gray_img = dummy_img

equalized_img = cv2.equalizeHist(gray_img)

plt.figure(figsize=(10, 8))

plt.subplot(2, 2, 1)
plt.imshow(gray_img, cmap='gray')
plt.title('Original Grayscale Image')
plt.axis('off')

plt.subplot(2, 2, 2)
plt.hist(gray_img.ravel(), 256, [0, 256], color='black')
plt.title('Histogram of Original Image')
plt.xlabel('Pixel Intensity')
plt.ylabel('Frequency')

plt.subplot(2, 2, 3)
plt.imshow(equalized_img, cmap='gray')
plt.title('Equalized Grayscale Image')
plt.axis('off')

plt.subplot(2, 2, 4)
plt.hist(equalized_img.ravel(), 256, [0, 256], color='black')
plt.title('Histogram of Equalized Image')
plt.xlabel('Pixel Intensity')
plt.ylabel('Frequency')

plt.tight_layout()
plt.show()
```
<img width="722" height="627" alt="image" src="https://github.com/user-attachments/assets/be76a5f3-5374-424b-a372-51dc52e62cc6" />

```
color_img = cv2.imread('/content/marvelous picture of spiderman.jpg')


if color_img is None:
    print("Error: 'parrot.jpg' could not be loaded for color processing. Creating a dummy color image.")
    dummy_color_img = np.zeros((100, 100, 3), dtype=np.uint8)
    for i in range(100):
        dummy_color_img[i, :, 0] = i * 2.55 # Red channel gradient
        dummy_color_img[i, :, 1] = 255 - (i * 2.55) # Green channel gradient
        dummy_color_img[:, i, 2] = i * 2.55 # Blue channel gradient
    color_img = dummy_color_img

color_img_rgb = cv2.cvtColor(color_img, cv2.COLOR_BGR2RGB)

b, g, r = cv2.split(color_img)

plt.figure(figsize=(6, 4))
plt.hist(b.ravel(), 256, [0, 256], color='blue', alpha=0.5, label='Blue')
plt.hist(g.ravel(), 256, [0, 256], color='green', alpha=0.5, label='Green')
plt.hist(r.ravel(), 256, [0, 256], color='red', alpha=0.5, label='Red')
plt.title('Histogram of B, G, R Channels')
plt.xlabel('Pixel Intensity')
plt.ylabel('Frequency')
plt.legend()
plt.show()
```
<img width="672" height="422" alt="image" src="https://github.com/user-attachments/assets/a12e4091-4c35-4a7b-9b29-b6f97f26a612" />

```
hsv_img = cv2.cvtColor(color_img, cv2.COLOR_BGR2HSV)

h, s, v = cv2.split(hsv_img)

v_equalized = cv2.equalizeHist(v)

hsv_equalized = cv2.merge([h, s, v_equalized])
enhanced_color_img = cv2.cvtColor(hsv_equalized, cv2.COLOR_HSV2BGR)
enhanced_color_img_rgb = cv2.cvtColor(enhanced_color_img, cv2.COLOR_BGR2RGB)

plt.figure(figsize=(10, 8))

plt.subplot(2, 2, 1)
plt.imshow(color_img_rgb)
plt.title('Original Color Image')
plt.axis('off')

plt.subplot(2, 2, 2)
plt.hist(color_img_rgb[:, :, 0].ravel(), 256, [0, 256], color='red', alpha=0.5, label='Red')
plt.hist(color_img_rgb[:, :, 1].ravel(), 256, [0, 256], color='green', alpha=0.5, label='Green')
plt.hist(color_img_rgb[:, :, 2].ravel(), 256, [0, 256], color='blue', alpha=0.5, label='Blue')
plt.title('Histogram of Original Color Image')
plt.legend()

plt.subplot(2, 2, 3)
plt.imshow(enhanced_color_img_rgb)
plt.title('Enhanced Color Image (HSV Equalization)')
plt.axis('off')

plt.subplot(2, 2, 4)
plt.hist(enhanced_color_img_rgb[:, :, 0].ravel(), 256, [0, 256], color='red', alpha=0.5, label='Red')
plt.hist(enhanced_color_img_rgb[:, :, 1].ravel(), 256, [0, 256], color='green', alpha=0.5, label='Green')
plt.hist(enhanced_color_img_rgb[:, :, 2].ravel(), 256, [0, 256], color='blue', alpha=0.5, label='Blue')
plt.title('Histogram of Enhanced Color Image')
plt.legend()

plt.tight_layout()
plt.show()
```
<img width="753" height="592" alt="image" src="https://github.com/user-attachments/assets/c4f50efd-c7fb-479c-8723-73797e7b5a3f" />

## Grayscale Histogram Equalization
- Original grayscale image is displayed
- Histogram of original grayscale image is plotted
- Enhanced image after histogram equalization is displayed
- Histogram of enhanced grayscale image shows improved contrast
## Color Image Histogram Equalization
- Original color image is displayed
- Histogram of B, G, R channels is plotted
- Enhanced image after HSV-based equalization is displayed
- Histogram of enhanced image shows better intensity distribution

## Result
Thus, histogram equalization is successfully performed on both grayscale and color images using OpenCV. The contrast and brightness of the images are significantly improved, enhancing visual quality and feature visibility.

