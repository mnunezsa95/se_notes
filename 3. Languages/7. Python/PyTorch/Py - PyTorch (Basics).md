See:
* [[Py - Introduction to Python]]
* [[Py - ML (ML for Texts)]]
Resources
* TripleTen Knowledge Base: [Data Science](https://tripleten.netlify.app/)
* Documentation: [PyTorch](https://pytorch.org/docs/stable/index.html)
---

# What is PyTorch?
* PyTorch is an open-source machine learning library primarily developed by Facebook's AI Research lab (FAIR). It is widely used for applications such as natural language processing and computer vision. Here are some key features and characteristics of PyTorch:
	1. **Tensors and Autograd**: PyTorch uses tensors, which are similar to NumPy arrays but can run on GPUs for faster computation. It also includes an automatic differentiation library called Autograd, which is crucial for training neural networks.
	
	2. **Dynamic Computation Graphs**: PyTorch builds dynamic computation graphs, meaning the graph is built on-the-fly as operations are executed. This is different from static computation graphs used in some other frameworks (like TensorFlow before version 2.0), making it more flexible and easier to debug.
	
	3. **TorchScript**: This feature allows you to transition seamlessly between eager mode (for immediate execution) and graph mode (for optimized execution), providing a good balance between ease of use and performance optimization.

	4. **Rich Ecosystem**: PyTorch has a rich ecosystem of tools and libraries for various tasks, including TorchVision for computer vision, TorchText for natural language processing, and PyTorch Geometric for graph neural networks.
	
	5. **Community and Support**: PyTorch has a large and active community, with extensive documentation, tutorials, and third-party resources available for learners and developers at all levels.

* In short, PyTorch is used for working with neural network models.

# Installing PyTorch
## Install using pip
* Installing PyTorch using the following bash command:
```bash
pip3 install torch torchvision torchaudio
```

## Install using Conda
```bash
curl -O https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-x86_64.sh
sh Miniconda3-latest-MacOSX-x86_64.sh
```

# Importing PyTorch
```Python
import torch
```