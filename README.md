# Histogram Equalization Using OpenCV (Grayscale & Color Images)

---

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
- OpenCV (`cv2`)  
- NumPy  
- Matplotlib  

---

## Algorithm

### Step 1:
Import the required libraries: OpenCV, NumPy, and Matplotlib.

### Step 2:
Read the image `parrot.jpg` in grayscale format.

### Step 3:
Display the grayscale image and plot its histogram.

### Step 4:
Apply histogram equalization using `cv2.equalizeHist()` to enhance contrast.

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
Name: SAFIRA BARVEEN S  

### Register No:
212224230235

### Grayscale Histogram Equalization

- Original grayscale image is displayed
 ```
  import cv2
import matplotlib.pyplot as plt

IMAGE_PATH = "Downloads/JET.jpg"

img = cv2.imread(IMAGE_PATH, cv2.IMREAD_GRAYSCALE)
if img is None:
    raise FileNotFoundError(f"Could not read image at '{IMAGE_PATH}'")

plt.imshow(img, cmap="gray", vmin=0, vmax=255)
plt.title("Original Grayscale Image")
plt.axis("off")
plt.show()
```

- Histogram of original grayscale image is plotted
```
import cv2
import matplotlib.pyplot as plt

IMAGE_PATH = "Downloads/JET.jpg"

img = cv2.imread(IMAGE_PATH, cv2.IMREAD_GRAYSCALE)
if img is None:
    raise FileNotFoundError(f"Could not read image at '{IMAGE_PATH}'")

plt.hist(img.ravel(), bins=256, range=(0, 256), color="gray")
plt.title("Histogram of Original Image")
plt.xlabel("Pixel intensity")
plt.ylabel("Frequency")
plt.show()
```
- Enhanced image after histogram equalization is displayed
```
import cv2

IMAGE_PATH = "Downloads/JET.jpg"

img = cv2.imread(IMAGE_PATH, cv2.IMREAD_GRAYSCALE)
if img is None:
    raise FileNotFoundError(f"Could not read image at '{IMAGE_PATH}'")

equalized = cv2.equalizeHist(img)
cv2.imwrite("equalized_output.png", equalized)

cv2.imshow("Equalized Image", equalized)
cv2.waitKey(0)
cv2.destroyAllWindows()
``` 
- Histogram of enhanced grayscale image shows improved contrast
```
import cv2
import matplotlib.pyplot as plt

IMAGE_PATH = "Downloads/JET.jpg"

img = cv2.imread(IMAGE_PATH, cv2.IMREAD_GRAYSCALE)
if img is None:
    raise FileNotFoundError(f"Could not read image at '{IMAGE_PATH}'")

equalized = cv2.equalizeHist(img)

plt.hist(equalized.ravel(), bins=256, range=(0, 256), color="gray")
plt.title("Histogram of Equalized Image")
plt.xlabel("Pixel intensity")
plt.ylabel("Frequency")
plt.show()
```  

### Color Image Histogram Equalization

- Original color image is displayed
```
import cv2
import numpy as np

IMAGE_PATH = "Downloads/JET.jpg"

img = cv2.imread(IMAGE_PATH, cv2.IMREAD_GRAYSCALE)
if img is None:
    raise FileNotFoundError(f"Could not read image at '{IMAGE_PATH}'")

equalized = cv2.equalizeHist(img)
comparison = np.hstack((img, equalized))
cv2.imwrite("comparison.png", comparison)

cv2.imshow("Original (left) | Equalized (right)", comparison)
cv2.waitKey(0)
cv2.destroyAllWindows()
``` 
- Histogram of B, G, R channels is plotted
```
import cv2
import matplotlib.pyplot as plt

IMAGE_PATH = "Downloads/JET.jpg"

img = cv2.imread(IMAGE_PATH, cv2.IMREAD_GRAYSCALE)
if img is None:
    raise FileNotFoundError(f"Could not read image at '{IMAGE_PATH}'")

equalized = cv2.equalizeHist(img)

fig, axes = plt.subplots(1, 2, figsize=(10, 4))

axes[0].hist(img.ravel(), bins=256, range=(0, 256), color="gray")
axes[0].set_title("Original Histogram")
axes[0].set_xlabel("Pixel intensity")
axes[0].set_ylabel("Frequency")

axes[1].hist(equalized.ravel(), bins=256, range=(0, 256), color="gray")
axes[1].set_title("Equalized Histogram")
axes[1].set_xlabel("Pixel intensity")
axes[1].set_ylabel("Frequency")

plt.tight_layout()
plt.show()
```
- Enhanced image after HSV-based equalization is displayed
```
import cv2

IMAGE_PATH = "Downloads/JET.jpg"

img = cv2.imread(IMAGE_PATH)
if img is None:
    raise FileNotFoundError(f"Could not read image at '{IMAGE_PATH}'")

ycrcb = cv2.cvtColor(img, cv2.COLOR_BGR2YCrCb)
ycrcb[:, :, 0] = cv2.equalizeHist(ycrcb[:, :, 0])
result = cv2.cvtColor(ycrcb, cv2.COLOR_YCrCb2BGR)

cv2.imwrite("color_equalized.png", result)
cv2.imshow("Original | Equalized", cv2.hconcat([img, result]))
cv2.waitKey(0)
cv2.destroyAllWindows()
``` 
- Histogram of enhanced image shows better intensity distribution
```
import cv2
import numpy as np

IMAGE_PATH = "Downloads/JET.jpg"

img = cv2.imread(IMAGE_PATH, cv2.IMREAD_GRAYSCALE)
if img is None:
    raise FileNotFoundError(f"Could not read image at '{IMAGE_PATH}'")

clahe = cv2.createCLAHE(clipLimit=2.0, tileGridSize=(8, 8))
clahe_img = clahe.apply(img)

cv2.imwrite("clahe_output.png", clahe_img)
cv2.imshow("Original | CLAHE", np.hstack((img, clahe_img)))
cv2.waitKey(0)
cv2.destroyAllWindows()
```



##  Output
<img width="970" height="557" alt="image" src="https://github.com/user-attachments/assets/88e8b7c5-cc9a-4cc8-bbd8-c2309d7a31e4" />
<img width="1047" height="553" alt="image" src="https://github.com/user-attachments/assets/ff4cfeed-f21e-478c-bb88-1545db07e33e" />

<img width="1060" height="586" alt="image" src="https://github.com/user-attachments/assets/9bab2173-ad5c-4c3f-9c47-8ba872274acc" />
<img width="1061" height="557" alt="image" src="https://github.com/user-attachments/assets/9b733bab-fd24-4369-bb39-5b1cd88e4658" />
<img width="1113" height="532" alt="image" src="https://github.com/user-attachments/assets/86eef615-b859-403a-a8ee-5dd4c3657bd7" />
<img width="1201" height="557" alt="image" src="https://github.com/user-attachments/assets/f5784d8e-50d3-445f-b1eb-3dc557e27813" />
<img width="1487" height="477" alt="image" src="https://github.com/user-attachments/assets/97174da0-2dd9-4633-97ed-c9a249a8dc3e" />
<img width="1440" height="397" alt="image" src="https://github.com/user-attachments/assets/f50a9713-b05f-46f9-be49-2a57613863b8" />

## Result

Thus, histogram equalization is successfully performed on both grayscale and color images using OpenCV. The contrast and brightness of the images are significantly improved, enhancing visual quality and feature visibility.
