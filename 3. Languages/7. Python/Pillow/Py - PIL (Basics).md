See:
* [[Py - Introduction to Python]]
* [[Py - PIL (Methods)]]
* [[Py - ML (Computer Vision)]]
Resources:
* Documentation: [Pillow](https://pillow.readthedocs.io/en/stable/)

---

# Introduction to Pillow (PIL) Library
* The Pillow library, often referred to as PIL (Python Imaging Library), is a popular Python library used for working with images. It provides extensive support for opening, manipulating, and saving many different image file formats. Pillow builds on top of the older PIL library, offering more features and improvements.
* Some common tasks you can perform with Pillow include:
	1. Opening and displaying images.
	2. Manipulating images by resizing, cropping, rotating, and flipping.
	3. Adding text and shapes to images.
	4. Applying various filters and enhancements to images.
	5. Saving images in different file formats.

* It's widely used in various applications such as image processing, computer vision, web development, and more, due to its simplicity and powerful capabilities.

# Installing Pillow
* Install Pillow with **pip**:
```bash
python3 -m pip install --upgrade pip
python3 -m pip install --upgrade Pillow
```

# Importing Pillow
* Import the entire library or necessary modules
```Python
# Import entire library
import PIL

# Import specific module
from PIL import Image
```