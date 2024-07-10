See:
* [[Py - Introduction to Python]]
* [[Py - PIL (Basics)]]
* [[Py - ML (Computer Vision)]]
Resources:
* Documentation: [Pillow](https://pillow.readthedocs.io/en/stable/)


---
# Modules

#### `Image`
* The Image module provides a class with the same name which is used to represent a PIL image. 
* The module also provides a number of factory functions, including functions to load images from files, and to create new images.
```Python
import numpy as np
from PIL import Image
import matplotlib.pyplot as plt

image = Image.open('/datasets/ds_cv_images/face.png')
array = np.array(image)

plt.imshow(array)
```