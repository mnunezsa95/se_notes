See:
* [[Py - Introduction to Python]]
* [[Py - TensorFlow (Basics)]]
* [[Py - TensorFlow (Methods)]]
* [[Py - ML (Computer Vision)]]
Resources:
* Documentation: [Keras](https://keras.io/getting_started/)
* Documentation: [TensorFlow](https://www.tensorflow.org/tutorials)


---
# Introduction to Keras
* Keras is a high-level interface of another more complex library, **TensorFlow.**
* Keras is a high-level neural networks API, written in Python and capable of running on top of TensorFlow, CNTK, or Theano. It's designed to enable fast experimentation with deep neural networks, focusing on ease of use, modularity, and extensibility.
* Here are some key points about Keras:
	1. **High-level API**: Keras provides a simple interface for creating and training neural networks. It allows you to define and manipulate neural networks using high-level building blocks.
	2. **Modularity**: Neural networks in Keras are constructed by connecting configurable building blocks together. Layers, optimizers, activation functions, and more can be easily combined to create new models.
	3. **Compatibility**: Keras can run on top of TensorFlow, CNTK, or Theano. TensorFlow 2.x includes Keras as part of its core API, making it the default high-level API for TensorFlow.
	4. **Ease of Use**: It simplifies the process of defining, training, and evaluating deep learning models. Its syntax is designed to be intuitive and expressive, enabling rapid prototyping and experimentation.
	5. **Flexibility**: Keras supports both convolutional networks for computer vision tasks and recurrent networks for sequence processing. It also allows for multi-input and multi-output models, as well as custom layers and loss functions.


# Installing Keras
* Install Keras from PyPI via:
```bash
pip install --upgrade keras
```

* Check the local Keras version number via:
```Python
import keras
print(keras.__version__)
```

* To use Keras 3, a backend framework – either JAX, TensorFlow, or PyTorch must be installed.
	* [Installing JAX](https://jax.readthedocs.io/en/latest/installation.html)
	* [Installing TensorFlow](https://www.tensorflow.org/install)
	* [Installing PyTorch](https://pytorch.org/get-started/locally/)


# Installing KerasCV and KerasNLP
* KerasCV and KerasNLP can be installed via pip:
```bash
pip install --upgrade keras-cv
pip install --upgrade keras-nlp
pip install --upgrade keras
```

# Configuring the Backend
* You can export the environment variable `KERAS_BACKEND` or you can edit your local config file at `~/.keras/keras.json` to configure your backend. 
* Available backend options are: `"jax"`, `"tensorflow"`, `"torch"``
```Bash
export KERAS_BACKEND="jax"
```

```Python
import os
os.environ["KERAS_BACKEND"] = "jax"
import keras
```