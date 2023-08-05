---
title: "Image Enhancement with Frequency Domain Filters"
summary: Application of Frequency Domain Filters for Image Clarity and License Plate Identification
draft: false
tags: ["Image Processing", "Frequency Domain Filters", "Computer-Vision", "Python"]

---

## Overview

This project focuses on implementing frequency domain filters to enhance image clarity, with a specific goal of identifying license plate numbers from noisy images. The Discrete Fourier Transform (DFT) and post-processing techniques are utilized to improve image contrast and suppress periodic noise.

![Original Image](/project_images/car.png)
##### *Caption: The original image of the car.*

### Image Preparation

The project starts with selecting a sample image of a car and converting it to grayscale, preparing it for frequency domain analysis.

### Frequency Domain Analysis

Using the DFT, the magnitude of the Fourier transform is calculated, and a logarithmic transformation is applied for effective visualization. White peaks in the Fourier domain indicate periodic noise in the image.

### Noise Suppression

To remove the periodic noise, a frequency domain filter is designed and tested with different filter sizes (2L+1 x 2L+1) to find the optimal configuration.

```python
# Python code for noise suppression using frequency domain filter

def noise_suppression(magnitude, coordinates, L):
    dx, dy = np.shape(magnitude)
    new = magnitude.copy()

    for coord in coordinates:
        i, j = coord[0], coord[1]
        if i == dx//2 and j == dy//2:
            continue
        else:
            for k1 in np.arange(-L, L, 1):
                for k2 in np.arange(-L, L, 1):
                    if i + k1 >= 0 and j + k2 >= 0 and i + k1 < dx and j + k2 < dy:
                        new[i + k1, j + k2] = 0
    return new

```

### Image Reconstruction
With the modified frequency components, the inverse Fourier transform is performed to reconstruct the enhanced image in the spatial domain.

### Contrast Enhancement
Histogram analysis of the reconstructed image intensities is performed, and an intensity transformation is applied to increase image contrast and improve the visibility of the license plate number.

```python
# Python code for contrast enhancement using intensity transformation

def intensity_scaling(img):
    img_back = np.abs(np.fft.ifft2(np.fft.ifftshift(img)))
    img_scaled = (img_back - np.min(img_back)) * 255.0 / (np.max(img_back) - np.min(img_back))
    return img_scaled
```

### Image Smoothing
Finally, an averaging filter is used for image smoothing, fine-tuning the image while minimizing noise artifacts.

### Conclusion

This project successfully demonstrates the application of frequency domain filters for image clarity enhancement and license plate identification in noisy images. The use of the Discrete Fourier Transform and post-processing techniques significantly improves image quality, making it a valuable tool for various image processing tasks.


![Final Image](/project_images/car1.png)

![Final Image](/project_images/car2.png)
