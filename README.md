#1   program to implement linear (Negative Transformation) and non-linear (Logarithmic and Power Law  
transformation) on gray scale images and comment on the results obtained.

import cv2
import numpy as np
import matplotlib.pyplot as plt

image = cv2.imread('input_image.jpg', cv2.IMREAD_GRAYSCALE)

negative = 255 - image
c = 255 / np.log(1 + np.max(image))

log_transformed = c * np.log(1 + image.astype(np.float32))
log_transformed = np.array(log_transformed, dtype=np.uint8)

gamma = 0.5
power_transformed = np.power(image / 255.0, gamma)
power_transformed = np.uint8(255 * power_transformed)

titles = ['Original', 'Negative', 'Logarithmic', 'Power Law (γ=0.5)']
images = [image, negative, log_transformed, power_transformed]

plt.figure(figsize=(10, 8))
for i in range(4):
    plt.subplot(2, 2, i+1)
    plt.imshow(images[i], cmap='gray')
    plt.title(titles[i])
    plt.axis('off')
plt.tight_layout()
plt.show()
