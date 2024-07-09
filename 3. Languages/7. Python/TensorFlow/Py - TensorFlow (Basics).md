See:
* [[Py - Introduction to Python]]
* [[Py - Keras (Basics)]]
* [[Py - TensorFlow (Methods)]]
* [[Py - ML (Computer Vision)]]
Resources:
* Documentation: [Keras](https://keras.io/getting_started/)
* Documentation: [TensorFlow](https://www.tensorflow.org/tutorials)


----
# Introduction to TensorFlow
* TensorFlow is an open-source machine learning framework developed by the Google Brain team. It is designed to facilitate the development and deployment of machine learning models, particularly deep learning models. 
* Here are some key features and components of TensorFlow:
	1. **Versatility**: TensorFlow supports a wide range of machine learning and deep learning tasks, including neural network training, natural language processing, computer vision, and more.
	2. **Tensor Operations**: At its core, TensorFlow operates on multidimensional arrays called tensors. These tensors flow through a series of operations, hence the name TensorFlow.
	3. **Graphs and Sessions**: TensorFlow initially used a static computational graph model, where you define the graph first and then execute it in a session. However, TensorFlow 2.x introduced eager execution, which allows operations to be evaluated immediately, making it more intuitive and easier to debug.
	4. **High-level APIs**: TensorFlow provides high-level APIs like Keras, which simplifies the process of building and training models. Keras is now the official high-level API of TensorFlow.
	5. **Scalability**: TensorFlow is designed to scale across multiple CPUs and GPUs, making it suitable for large-scale machine learning tasks.
	6. **Deployment**: TensorFlow models can be deployed in various environments, from cloud servers to edge devices, making it versatile for different applications.
	7. **Support for Different Languages**: While primarily used with Python, TensorFlow also supports other languages like C++, JavaScript, and Java, making it accessible to a broader range of developers.

# TensorFlow for MacOS
* There is currently no official GPU support for MacOS.

# Installing TensorFlow
* Check Python version
```bash
python3 --version
python3 -m pip --version
```
* Upgrade pip installation to ensure latest version
```bash
pip install --upgrade pip
```
* Install TensorFlow
```bash
python3 -m pip install tensorflow
```
* Verify the installation
```Bash
python3 -c "import tensorflow as tf; print(tf.reduce_sum(tf.random.normal([1000, 1000])))"
```