## DIPT-Ex-7

# Detect-the-lines-using-Hough-Transform
# Lane Detection
# AIM:
To implement a basic lane detection pipeline using OpenCV by completing missing code segments at specified locations.
# Learning Objective:
1.Understand each stage of image processing

2.Learn how to build a complete computer vision pipeline

3.Practice writing code in guided sections

# Software Used
Anaconda – Python 3.7

Jupyter Notebook / VS Code

OpenCV (cv2)

NumPy

Matplotlib

# Algorithm & Explanation
# Step 1: Import Libraries
```
import cv2
import numpy as np
import matplotlib.pyplot as plt
```
# Step 2: Read the Image
```
img = cv2.imread("building.jpg")

if img is None:
    print("Error: Image not found. Check the image path.")
else:
    print("Image loaded successfully")
```
# Step 3: Convert to Grayscale
```
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

plt.imshow(gray, cmap="gray")
plt.title("Grayscale Image")
plt.axis("off")
plt.show()
```
# Step 4: Display Images
```
plt.figure(figsize=(10, 5))

plt.subplot(1, 2, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis("off")

plt.subplot(1, 2, 2)
plt.imshow(gray, cmap="gray")
plt.title("Grayscale Image")
plt.axis("off")

plt.show()
```
# Step 5: Thresholding
```
ret, threshold = cv2.threshold(
    gray,
    127,
    255,
    cv2.THRESH_BINARY
)

plt.imshow(threshold, cmap="gray")
plt.title("Thresholded Image")
plt.axis("off")
plt.show()
```
# Step 6: Region of Interest (ROI)
```
height, width = gray.shape

mask = np.zeros_like(gray)

polygon = np.array([[
    (0, height),
    (width, height),
    (int(width * 0.6), int(height * 0.55)),
    (int(width * 0.4), int(height * 0.55))
]], dtype=np.int32)

cv2.fillPoly(mask, polygon, 255)

roi = cv2.bitwise_and(threshold, mask)

plt.imshow(roi, cmap="gray")
plt.title("Region of Interest")
plt.axis("off")
plt.show()
```
# Step 7: Edge Detection (Canny)
```
edges = cv2.Canny(roi, 50, 150)

plt.imshow(edges, cmap="gray")
plt.title("Canny Edge Detection")
plt.axis("off")
plt.show()
```
# Step 8: Gaussian Blur
```
blur = cv2.GaussianBlur(
    edges,
    (5, 5),
    0
)

plt.imshow(blur, cmap="gray")
plt.title("Gaussian Blur")
plt.axis("off")
plt.show()
```
# Step 9: Hough Transform
```
lines = cv2.HoughLinesP(
    blur,
    1,
    np.pi / 180,
    threshold=50,
    minLineLength=50,
    maxLineGap=100
)

print("Detected Lines:", lines)
```
# Step 10: Lane Detection Logic
```
lane = cv2.cvtColor(
    img,
    cv2.COLOR_BGR2RGB
).copy()

if lines is not None:

    for line in lines:

        line = np.array(line).reshape(-1)

        if len(line) == 4:

            x1, y1, x2, y2 = line

            cv2.line(
                lane,
                (int(x1), int(y1)),
                (int(x2), int(y2)),
                (255, 0, 0),
                5
            )

plt.figure(figsize=(10, 6))
plt.imshow(lane)
plt.title("Final Lane Detection")
plt.axis("off")
plt.show()
```
# Output:
# original image:

<img width="179" height="140" alt="image" src="https://github.com/user-attachments/assets/2c2d7ef6-8467-4e43-ae83-3d8879d72cd9" />

# Grayscale image:

<img width="350" height="272" alt="image" src="https://github.com/user-attachments/assets/759bab48-c835-405d-94a4-17687e549cb0" />


# Thresholded image:
<img width="317" height="265" alt="image" src="https://github.com/user-attachments/assets/34813e9e-cb67-4637-8545-02260f761209" />


# ROI image:

<img width="367" height="281" alt="image" src="https://github.com/user-attachments/assets/e7a14b88-fa02-4b90-a089-0d3392140ef3" />


# Edge detected image:

<img width="358" height="272" alt="image" src="https://github.com/user-attachments/assets/081784e8-8a9a-4d09-81a8-b31e014435ed" />


# Gaussian blur:

<img width="347" height="275" alt="image" src="https://github.com/user-attachments/assets/65508b5c-fd04-437a-a898-d7dda85c5c24" />


# Final lane detection:
<img width="446" height="353" alt="image" src="https://github.com/user-attachments/assets/3e30529e-6079-48b7-894f-7772e6f716c1" />


# Result:
Thus, the lane detection pipeline is successfully implemented by completing the missing code sections. The system detects and highlights lane lines effectively.
