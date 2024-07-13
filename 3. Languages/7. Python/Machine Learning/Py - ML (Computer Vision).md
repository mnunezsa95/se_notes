See:
* [[Py - Introduction to Python]]
* [[Py - PIL (Basics)]]
* [[Py - PIL (Methods)]]
* [[Py - TensorFlow (Basics)]]
* [[Py - TensorFlow (Methods)]]
* [[Py - Pandas (Basics)]]
* [[Py - Matplotlib (Methods)]]

Resources:
* TripleTen Knowledge Base: [Data Science](https://tripleten.netlify.app/)
* Documentation: [Pandas](https://pandas.pydata.org/docs/)
* Documentation: [NumPy](https://numpy.org/doc/stable/index.html)
* Documentation: [SK-Learn](https://scikit-learn.org/stable/)
* Documentation: [SciPy](https://docs.scipy.org/doc/scipy/index.html)
* TensorFlow Digital Playground: 
	* [Exercise 1](https://playground.tensorflow.org/#activation=sigmoid&batchSize=10&dataset=xor&regDataset=reg-plane&learningRate=0.00001&regularizationRate=0&noise=0&networkShape=5&seed=0.79032&showTestData=false&discretize=false&percTrainData=50&x=true&y=true&xTimesY=false&xSquared=false&ySquared=false&cosX=false&sinX=false&cosY=false&sinY=false&collectStats=false&problem=classification&initZero=false&hideText=false)
	* [Exercise 2](https://playground.tensorflow.org/#activation=sigmoid&batchSize=10&dataset=circle&regDataset=reg-plane&learningRate=0.03&regularizationRate=0&noise=0&networkShape=&seed=0.39605&showTestData=false&discretize=false&percTrainData=50&x=true&y=true&xTimesY=false&xSquared=false&ySquared=false&cosX=false&sinX=false&cosY=false&sinY=false&collectStats=false&problem=classification&initZero=false&hideText=false)
	* [Exercise 3](https://playground.tensorflow.org/#activation=sigmoid&batchSize=10&dataset=circle&regDataset=reg-plane&learningRate=0.03&regularizationRate=0&noise=0&networkShape=&seed=0.39605&showTestData=false&discretize=false&percTrainData=50&x=true&y=true&xTimesY=false&xSquared=false&ySquared=false&cosX=false&sinX=false&cosY=false&sinY=false&collectStats=false&problem=classification&initZero=false&hideText=false)
	* [Exercise 4](https://playground.tensorflow.org/#activation=sigmoid&batchSize=10&dataset=circle&regDataset=reg-plane&learningRate=0.1&regularizationRate=0&noise=0&networkShape=4,4,4,4&seed=0.29689&showTestData=false&discretize=false&percTrainData=50&x=true&y=true&xTimesY=false&xSquared=false&ySquared=false&cosX=false&sinX=false&cosY=false&sinY=false&collectStats=false&problem=classification&initZero=false&hideText=false)
	* [Exercise 5](https://playground.tensorflow.org/#activation=sigmoid&batchSize=10&dataset=spiral&regDataset=reg-plane&learningRate=0.03&regularizationRate=0&noise=0&networkShape=&seed=0.37123&showTestData=false&discretize=false&percTrainData=50&x=true&y=true&xTimesY=false&xSquared=false&ySquared=false&cosX=false&sinX=false&cosY=false&sinY=false&collectStats=false&problem=classification&initZero=false&hideText=false)
* Practice Sets: Training Multilayer Network
	* [train_features.npy](https://practicum-content.s3.us-west-1.amazonaws.com/data-eng/datasets/train_features.npy)
	* [train_target.npy](https://practicum-content.s3.us-west-1.amazonaws.com/data-eng/datasets/train_target.npy)
	* [test_features.npy](https://practicum-content.s3.us-west-1.amazonaws.com/data-eng/datasets/test_features.npy)
	* [test_target.npy](https://practicum-content.s3.us-west-1.amazonaws.com/data-eng/datasets/test_target.npy)
* GitHub: [The Adam Algorithm](https://gist.github.com/EmilienDupont/aaf429be5705b219aaaf8d691e27ca87/#file-thumbnail-png)



---

# Intro to Computer Vision
## What is Computer Vision?
* **Computer vision** is a field of artificial intelligence that tries to mimic human vision.

# Tasks with Neural Networks
## Intro to Neural Network Tasks
- Linear regression, random forest, and gradient boosting are effective for tabular data, where each row represents an observation and columns store features.
- Type of tasks for Neural Networks
	- Images
	- Video
	- Audio
	- Chat Bots
- Different tasks require different approaches for machine learning.
	- When dealing with other types of data, such as images, alternative approaches are necessary.
		- Example: Images
		    - One common approach involves converting pixel values into a vector to represent the features.
			    `[255, 255, 255, 255, 237, 217, 239, 255, 255, 255, 255, 255, 255, 255, 255, 190, 75, 29, 29, 30, 81, 198, 255, 255, 255...]`
			* Classic Algorithms (gradient boosting, n-grams, bag-of-words, etc) won't work due to the amount of features

## Similarities and Differences in Images and Text
* Similarities between Images and Text:
	* **Redundancy in Information**:
	    - Images: Background pixels are less important than pixels depicting details like wrinkles or gray hair for age determination.
	    - Texts: Prepositions and conjunctions carry less meaning compared to verbs and nouns.
	- **Relationships Between Features**:
	    - Images: Adjacent pixels often belong to the same object.
	    - Texts: Neighboring words in a sentence are related in meaning.
* Differences between Images and Text:
	- **Impact of Shuffling**:
	    - Tabular Data: Shuffling columns doesn't change the data's meaning.
	    - Images: Shuffling pixels introduces noise and alters the image.

## Role of Neural Networks
* Neural Networks help process large feature sets efficiently, considering both the significance of features and their sequential relationships.


# The TensorFlow & Keras Library
## Intro to TensorFlow / Keras
* The Keras Library is built as an interface for the TensorFlow Library, which is used for neural network models.

## Understanding Neural Networks
- A **Layer** consists of neurons that have identical inputs and outputs.
- A **Fully Connected Layer** is a layer where all inputs are connected to all neurons (or outputs)
- A **Neuron** represents the value at a single output.
    - Each neuron receives $n$ inputs, each of which is multiplied by its corresponding weight (e.g., $x_i$ is multiplied by $w_i$).
    - Each neuron also has an additional output known as the bias (denoted as $b$).
        - The bias is always set to one.
	![[neural-network-visual-input-ouput.png]]

# Linear Regression in Computer Vision

## Linear Regression in Keras
* The `Seqeutnal()` class is used for models with sequential layers. 
* The **`keras.layers.Dense()`** command creates one layer of neurons.
	* "Dense" means that every input will be connected to every neuron, or output.
	* The **`units`** parameter sets the number of neurons in the layer
	* The **`input_dim`** sets the number of inputs in the layer.
* The `model.add()` method adds the fully connected layer to the model
* The `model.compile()` method prepares the model for training
	* The `loss` parameter specifies the regression task loss function
	* The `optimizer='sgd'` parameter sets the gradient descent method
```Python
import pandas as pd
from tensorflow import keras # Import Keras from Tensorflow library

data = pd.read_csv('/datasets/train_data_n.csv')
features = data.drop('target', axis=1)
target = data['target']

# Initialize the model (ex: the neural network that will be built).
## Sequential() class is used for models with sequential layers
### A Layer is a set of neurons that share the same input & output
model = keras.models.Sequential()

# Indicate how the neural network is arranged
## The model.add() adds the fully connected layer to the model
## The keras.layers.Dense() command creates one layer of neurons.
### "Dense" means that every input is connected to every neuron, (or output).
### The units parameter sets the number of neurons in the layer
### The input_dim sets the number of inputs in the layer.
model.add(keras.layers.Dense(units=1, input_dim=features.shape[1]))

# Indicate how the neural network is trained
## Specifies MSE as the regression task loss function. 
## Sets the gradient descent method
model.compile(loss='mean_squared_error', optimizer='sgd')

# Train the model
model.fit(features, target)
```

```Python
# Example 
import pandas as pd
from tensorflow import keras

data_train = pd.read_csv('/datasets/train_data_n.csv')
features_train = data_train.drop('target', axis=1)
target_train = data_train['target']

data_valid = pd.read_csv('/datasets/test_data_n.csv')
features_valid = data_valid.drop('target', axis=1)
target_valid = data_valid['target']

model = keras.models.Sequential()

model.add(keras.layers.Dense(
	units=1, input_dim=features_train.shape[1])
)

model.compile(loss='mean_squared_error', optimizer='sgd')

model.fit(
	features_train, 
	target_train, 
	verbose=2, 
	epochs=5, 
	validation_data=(features_valid, target_valid)
)
```

```Result
Epoch 1/5
32/32 - 1s - loss: 9.1966 - val_loss: 7.3274 - 670ms/epoch - 21ms/step

Epoch 2/5
32/32 - 0s - loss: 7.1577 - val_loss: 6.8168 - 94ms/epoch - 3ms/step

Epoch 3/5
32/32 - 0s - loss: 6.6678 - val_loss: 6.7290 - 116ms/epoch - 4ms/step

Epoch 4/5
32/32 - 0s - loss: 6.4904 - val_loss: 6.7321 - 86ms/epoch - 3ms/step

Epoch 5/5
32/32 - 0s - loss: 6.4733 - val_loss: 6.7473 - 85ms/epoch - 3ms/step
```


# Logistic Regression in Computer Vision
* Linear regression and Logistic Regression are neural networks with only one neuron.
* What are the differences between linear and logistic regressions with only one neuron?
	* Linear Regression
		![[linear-regression-neural-network.png]]
	* Logistic Regression
		* Logistic Regression has a **sigmoid function** (or activation function)
			* The Sigmoid Function is a function that outputs values ranging from 0 to 1. 
			* Formula for Sigmoid Function: 
				* Euler's number ($e$) = ~2.718281828 $$sigma(z) = 1 / (1+e^-z)$$
		![[logistic-regression-neural-network.png]]

## The Sigmoid Function
### What is the Sigmoid Function?
- The Sigmoid Function is a function that outputs values ranging from 0 to 1.
- This output can be interpreted as a neural network's prediction of whether an observation belongs to the positive or negative class.

### Interpreting the Sigmoid Function
* If the sum of the products of the inputs' values and the weights (z) is a large positive number, then at the sigmoid output, we get a number close to unity:
		![[sigmoid-output-close-to-unity.png]]
* If the sum of the products of the inputs' values and the wights (z) is a large negative number, then the function returns a number close to zero
		![[sigmoid-output-close-to-0.png]]

## Loss Function in Logistic Regression 
* The Loss Function depends on the neural network type:
	* Regression Tasks -- Uses Mean Square Error (MSE)
	* Binary Classification Tasks -- Uses **Binary Cross Entropy (BCE)**

### Binary Cross Entropy (BCE)
#### BCE Fomula
* Formula: 
	* $p$ -- the probability of getting a correct answer.
	* If the target = 1, then p is: $$p = sigma(z)$$
	* If the target = 0, then p is: $$p = (1 - sigma(z))$$
$$BCE = -log(p)$$

#### Understanding BCE Value
* If the probability $p$ of the correct answer is close to one, then $−log⁡(p)$ is a small positive number near zero, indicating a small error.
* If the probability $p$ of the correct answer is close to zero, then $−log⁡(p)$ is a large positive number, indicating a large error.
	![[bce-graphical-interpretation.png]]

## Logistic Regression in Keras
* Using Logistic Regression in Keras involves a process similar to Linear Regression, with a few key differences:
	- Set the activation function to `'sigmoid'` using the `activation=` parameter.
	- Set the loss function to `'binary_crossentropy'` in the `model.compile()` method.
	- Set the optimizer to `'sgd'` in the `model.compile()` method.
```Python
# Example -- Logistic Regression in Keras

import pandas as pd
from tensorflow import keras

# Import train data
df = pd.read_csv('/datasets/train_data_n.csv')

# Create Target column for train data
df['target'] = (df['target'] > df['target'].median()).astype(int)

# Define Train features & target
features_train = df.drop('target', axis=1)
target_train = df['target']

# Import validation data
df_val = pd.read_csv('/datasets/test_data_n.csv')

# Create Target column for validation data
df_val['target'] = (
	df_val['target'] > df['target'].median()
).astype(int)

# Define Validation features & target
features_valid = df_val.drop('target', axis=1)
target_valid = df_val['target']

# Create the model
model = keras.models.Sequential()

# Create a layer and add the layer
model.add(
	keras.layers.Dense(
		units=1, 
		input_dim=features_train.shape[1],
		activation='sigmoid'
	)
)

# Prepare model for training
model.compile(loss='binary_crossentropy', optimizer='sgd')

# Train the model
model.fit(features_train, target_train, verbose=10, 
		  epochs=5, validation_data=(features_valid, target_valid)
)

# Predict with model
pred_valid = model.predict(features_valid) > 0.5

# Find accuracy
score = accuracy_score(target_valid, pred_valid)
print('Accuracy:', score)
```

```Result 
1/32 [..............................] - ETA: 1s
32/32 [==============================] - 0s 1ms/step
Accuracy: 0.501
```

```Python
# Example -- Using the metrics= parameter to trace quality at different epochs

import pandas as pd
from tensorflow import keras
from sklearn.metrics import accuracy_score

# Import train data
df = pd.read_csv('/datasets/train_data_n.csv')

# Create Target column for train data
df['target'] = (df['target'] > df['target'].median()).astype(int)

# Define train features & target
features_train = df.drop('target', axis=1)
target_train = df['target']

# Import validation data
df_val = pd.read_csv('/datasets/test_data_n.csv')

# Create Target column for validation data
df_val['target'] = (df_val['target'] > df['target'].median()).astype(int)

# Define Validation features & target
features_valid = df_val.drop('target', axis=1)
target_valid = df_val['target']

# Create the model
model = keras.models.Sequential()

# Create a layer and add the layer
model.add(
    keras.layers.Dense(
        units=1, input_dim=features_train.shape[1], activation='sigmoid'
    )
)

# Prepare model for training
model.compile(loss='binary_crossentropy', optimizer='sgd', metrics=['acc'])

# Train the model
model.fit(features_train, target_train, epochs=10, verbose=2,
          validation_data=(features_valid, target_valid))
```

```Result
Epoch 1/10
32/32 - 1s - loss: 0.8950 - acc: 0.4990 - val_loss: 0.8954 - val_acc: 0.4850 - 829ms/epoch - 26ms/step
Epoch 2/10
32/32 - 0s - loss: 0.8601 - acc: 0.5160 - val_loss: 0.8708 - val_acc: 0.4850 - 94ms/epoch - 3ms/step
Epoch 3/10
32/32 - 0s - loss: 0.8292 - acc: 0.5200 - val_loss: 0.8498 - val_acc: 0.4880 - 97ms/epoch - 3ms/step
Epoch 4/10
32/32 - 0s - loss: 0.8017 - acc: 0.5290 - val_loss: 0.8299 - val_acc: 0.4840 - 120ms/epoch - 4ms/step
Epoch 5/10
32/32 - 0s - loss: 0.7766 - acc: 0.5430 - val_loss: 0.8127 - val_acc: 0.4850 - 94ms/epoch - 3ms/step
Epoch 6/10
32/32 - 0s - loss: 0.7556 - acc: 0.5550 - val_loss: 0.7975 - val_acc: 0.4940 - 96ms/epoch - 3ms/step
Epoch 7/10
32/32 - 0s - loss: 0.7366 - acc: 0.5630 - val_loss: 0.7842 - val_acc: 0.4980 - 91ms/epoch - 3ms/step
Epoch 8/10
32/32 - 0s - loss: 0.7200 - acc: 0.5710 - val_loss: 0.7732 - val_acc: 0.5080 - 93ms/epoch - 3ms/step
Epoch 9/10
32/32 - 0s - loss: 0.7059 - acc: 0.5880 - val_loss: 0.7635 - val_acc: 0.5070 - 98ms/epoch - 3ms/step
Epoch 10/10
32/32 - 0s - loss: 0.6932 - acc: 0.5930 - val_loss: 0.7551 - val_acc: 0.5140 - 120ms/epoch - 4ms/step
```


# Fully Connected Neural Networks
## What is a Fully Connect Neural Network?
* In a Fully Connected Neural Network, every neuron in each layer is connect with each neuron in adjacent layers
	* Layers between the input and output layers are called **hidden layers**
	![[fully-connected-neural-network.png]]

## Structure of Fully Connected Neural Networks
* Every neuron, except for the last neuron is followed by an activation function
		![[structure-fully-connected-neural-network.png]]
	* To find the z, sum all products of the inputs values and the weights $$z1 = (x1 * w11) + (x2*w12)$$ $$z2= (x1 * w21) + (x2*w22)$$$$z3=(z1 * w31) + (z2*w32)$$ 
		* Which can be simplified: $$z3 = (x1 * w11 + x2 * w12) * w31 + (w21 * x1 + w22 * x2) * w32$$
		* Take $x1$ and $x2$ out of the brackets: $$z3 = x1 * (w11 * w31 + w21 * w32) + x2 * (w12 * w31 + w22 * w32)$$
		* Add the new notation $w1'$ and $w2'$ $$w1' = w11 * w31 + w21 * w32$$ $$w2' = w12 * w31 + w22 * w32$$
		* Which can be simplified: $$z3 = (\;x1 * w1'\;) + (\;x2 * w2'\;)$$
		* The simplified diagram: 
			* A multilayer network is a single neuron network
			![[simplified-fully-connected-neural-network.png]]
	* Reintroducing the sigmoid to see how the network changes:
		![[fully-connected-neural-network-sigmoid.png]]
		* The formula: $$z1 = σ(x1 * w11 + x2 * w12)$$ $$z2 = σ(x1 * w21 + x2 * w22)$$ $$z3 = z1 * w31 + z2 * w32$$
			* Which can be simplified: $$z3 =  σ(x1 * w11 + x2 * w12) * w31 + σ(w21 * x1 + w22 * x2) * w32$$

## How Neural Networks are Trained
### Training and Parameters in Multilayer Networks
- Multilayer networks are trained using gradient descent.
- The parameters are the weights of neurons in each fully connected layer.
	- Changing the parameters (learning rate, epochs, step size, activation function, batch size, etc) can make training more efficient.
	- Other features (number of neurons, number of layers) can make training more efficient or less efficient 
- The training objective is to find the parameters that minimize the loss function.

### The Impact of Activation Function on Training
- A **linear** activation function (essentially no activation) is not effective in minimizing the loss function.
- A **sigmoid** activation function is more effective in minimizing the loss function.
    - However, as the number of layers increases, training becomes less efficient due to a **vanishing signal** caused by the sigmoid activation function.
        - A **vanishing signal** occurs when there are too many layers, reducing the amount of signal that propagates from the input to the output.
        - The sigmoid function repeatedly converts large values into smaller ones, leading to a **vanishing signal**.
* A **ReLU (Rectified Linear Unit)** activation function addresses the **vanishing signal** problem.
	- **ReLU** sets all negative values to 0 and leaves positive values unchanged.
	- **ReLU** is effective for training many layers and generally only encounters problems when the number of layers reaches the dozens.
	- ReLU visual:
		![[relu-activiation-function-visual.png]]
	* ReLU Formula: $$ReLU(x) = max(0,x)$$

## Fully Connected Neural Networks in Keras
* A Fully Connected Neural Network is very similar to a single layer neural network. 
	* To create more than one layer, the `keras.layers.Dense()` more than once.
```Python
import pandas as pd
from tensorflow import keras
from sklearn.metrics import accuracy_score

df = pd.read_csv('/datasets/train_data_n.csv')
df['target'] = (df['target'] > df['target'].median()).astype(int)
features_train = df.drop('target', axis=1)
target_train = df['target']

df_val = pd.read_csv('/datasets/test_data_n.csv')
df_val['target'] = (df_val['target'] > df['target'].median()).astype(int)
features_valid = df_val.drop('target', axis=1)
target_valid = df_val['target']

model = keras.models.Sequential()

# Adding two layers
model.add(keras.layers.Dense(units=10, activation='sigmoid'))
model.add(keras.layers.Dense(units=1, activation='sigmoid'))

# Prepare the model for training
model.compile(loss='binary_crossentropy', optimizer='sgd', metrics=['acc'])

# Training the model
model.fit(features_train, target_train, epochs=10, verbose=2,
          validation_data=(features_valid, target_valid))
```


# Working with Images in Python
* Python has a dedicated library called Pillow or PIL(Python Imaging Library) for working with images.
## The Python Imaging Library (PIL)
### The Image Module
* The PIL Library has an `Image` module provides a number of factory functions, including functions to load images from files, and to create new images.
	* The `open()` method is used to load an image in Python
	* The `NumPy` library can be used to convert the image into an array
	* The `matplotlib` library can be used to plot the the image
```Python
import numpy as np
from PIL import Image

# Load the image
image = Image.open('/datasets/ds_cv_images/face.png')

# Convert the image into an array
array = np.array(image)
print(array)

# Change the color map of the image
plt.imshow(array, cmap='gray')

# Plot the image
plt.colorbar()
```

```Result
[[255 255 255 255 237 217 239 255 255 255 255 255 255]
 [255 255 190  75  29  29  30  81 198 255 255 255 255]
 [255 147  30  29  29  29  29  29  31 160 255 255 255]
...
 [ 29  38 180 255 255 255 255 255 169  35  29  29  29]
 [ 29  29  29  82 153 174 150  76  29  29  29  29  29]
 [ 29  29  29  29  29  29  29  29  29  29  29  29  29]]
```


## Black and White Images
* Black and White images are two-dimensional arrays with cells containing integers from 0 to 255
* Neural networks learn better when they receive images in the range from 0 to 1 as input.
```Python
# Example --- Adjusting color value of the image

import numpy as np
from PIL import Image
import matplotlib.pyplot as plt

image = Image.open('/datasets/ds_cv_images/face.png')
array = np.array(image)

# Repainting the upper left corner of the image black (0), and the lower right corner white (255)
array[14, 12] = 255
array[0, 0] = 0

plt.imshow(array, cmap='gray')
plt.colorbar()
```

* Neural networks learn better when they receive images in the range from 0 to 1 as input.
```Python
# Example --- Change the array input ranges

import numpy as np
from PIL import Image
import matplotlib.pyplot as plt

image = Image.open('/datasets/ds_cv_images/face.png')
array = np.array(image)

# Divide every value in the array by 255
print(array)
array = array / 255
print(array)

plt.imshow(array, cmap='gray')
plt.colorbar()
```

```Result
[[255 255 255 255 237 217 239 255 255 255 255 255 255] [255 255 190 75 29 29 30 81 198 255 255 255 255] [255 147 30 29 29 29 29 29 31 160 255 255 255] [185 29 29 29 29 29 29 29 29 31 198 255 255] [ 61 29 29 29 29 29 29 29 29 29 74 255 255] ...
[ 30 187 255 234 218 218 218 218 243 174 29 29 29] [ 29 38 180 255 255 255 255 255 169 35 29 29 29] [ 29 29 29 82 153 174 150 76 29 29 29 29 29] [ 29 29 29 29 29 29 29 29 29 29 29 29 29]] 


[[1. 1. 1. 1. 0.92941176 0.85098039 0.9372549 1. 1. 1. 1. 1. 1. ] [1. 1. 0.74509804 0.29411765 0.11372549 0.11372549 0.11764706 0.31764706 0.77647059 1. 1. 1. 1. ] [1. 0.57647059 0.11764706 0.11372549 0.11372549 0.11372549 0.11372549 0.11372549 0.11372549 0.11372549 0.11372549 0.11372549 0.11372549 0.12156863 
...
[0.11372549 0.14901961 0.70588235 1. 1. 1. 1. 1. 0.6627451 0.1372549 0.11372549 0.11372549 0.11372549] [0.11372549 0.11372549 0.11372549 0.11372549 0.11372549 0.11372549 0.11372549 0.11372549 0.11372549 0.11372549 0.11372549]]
```

## Color Images
* Color images, also known as RGB images, are represented as three-dimensional arrays where each cell contains integers ranging from 0 to 255.
	* These images consist of three channels: red, green, and blue.
		* The 1st coordinate is the row ID
		* The 2nd coordinate is the column ID
		* The 3rd coordinate is the column Channel
		![[color-image-composition.png]]

- Three-dimensional arrays (and Images) in NumPy work similarly to two-dimensional arrays.
	- Each pixel within these arrays stores three numbers, representing the brightness levels of the red, green, and blue channels.
```Python
# Creating a two-dimensional array

np.array([[0, 255], [255, 0]])

# Creating a three-dimensional array
np.array([[[0, 255, 0], [128, 0, 255]], [[12, 89, 0], [5, 89, 245]]])
```

```Python
# Example -- Working with an RGB image

# Import libraries
from PIL import Image
import numpy as np
import matplotlib.pyplot as plt

# Load the image
image = Image.open('/datasets/ds_cv_images/cat.jpg')

# Convert the image into an array
array = np.array(image)

# Print the size of the array (to verify the chanlles are stored in third coordinate)
print(array.shape) # (300, 400, 3)

# Get the output of the red channel only
red_channel = array[:, :, 0]

# Print the output of red channel
print(red_channel)

# Plot the image
plt.imshow(array)

# Plot the image
plt.colorbar()
```

```Result
# Output of the red channel 

[[115 111 111 ... 119 117 117]
 [115 113 114 ... 119 118 118]
 [115 115 117 ... 122 122 122]
 ...
 [179 180 176 ... 197 195 197]
 [176 178 173 ... 197 194 196]
 [173 174 170 ... 196 195 197]]
```


# Multiclass Classification
## What is Multiclass Classification?
* An observation can belong to one of several classes (not just two classes)
* In a multiclass classification, there are more than one output neurons, where each neuron is responsible for its own class
		![[multiclass-classification-visual.png]]

## Working with Multiclass Classifications
* Multiclass classifications utilize the **SoftMax** activation function instead of sigmoid because it ensures that probabilities sum up to 1.
	- SoftMax takes multiple network outputs and transforms them into probabilities that collectively add up to one.
	- To apply **SoftMax**, all output values are required.
	    - The number of neurons in the output layer corresponds to the number of classes, with each output connected to SoftMax.
	- Formula:
	    - Each probability is computed by dividing Euler's number raised to the power of the output weight by the sum of all probabilities.$$SoftMax(z_i) = (exp(z_i)) / (sum_i exp(z_i)) $$

### Example: A Multiclass Classification
* Image the following neural network
		![[multiclass-classification-visual-softmax.png]]
	* Calculate the probably of each neuron using the SoftMax activation function
	$$p_1 = (e_1^z) / (e^z_1 + e^z_2 + e^z_3)$$$$p_2 = (e_2^z) / (e^z_1 + e^z_2 + e^z_3)$$$$p_3 = (e_3^z) / (e^z_1 + e^z_2 + e^z_3)$$
	* Can be simplified as: 
		* If z₁ is significantly greater than z₂ and _z₃_, then in formula $e^z_1 / (e^z_1 + e^z_2 + e^z_3)$ the numerator is approximately equal to the denominator, that is $p₁≈1$
		* If _z₁_ is significantly less than _z₂_ or _z₃_, then in formula $e^z_1 / (e^z_1 + e^z_2 + e^z_3)$ the numerator is much less than the denominator, that is $p₁≈0$ $$p_1 + p_2 + p_3 = SoftMax(z_1) + SoftMax(z_2) + SoftMax(z_3) = (e_1^z) / (e^z_1 + e^z_2 + e^z_3) + (e_2^z) / (e^z_1 + e^z_2 + e^z_3) + (e_3^z) / (e^z_1 + e^z_2 + e^z_3) = 1$$


## Multiclass Classification in Keras
- How does Multiclass Classification work in Keras?
	- During training, probabilities generated by SoftMax are fed into the cross-entropy function to compute the error.
	- The gradient descent method is then employed to minimize the loss function.
	- The only condition for gradient descent to function effectively is that the function must have derivatives with respect to all parameters: weights and biases of the neural network.
- Training with Multiclass Classification
	- Transform the features from a 3D array to a 2D table (using NumPy's `reshape()` method)
		- Why? --> In a fully connected network, the input observations should be the rows of the table, and the whole dataset should be a two-dimensional table.
	- When creating and adding the layer
		- Use `activation='softmax'` when creating and adding the layer
		- The `input_dim=` is the size of the second and third value
	- When preparing the model for training
		- Use `loss='sparse_categorical_crossentropy'`
	- 
```Python
from tensorflow import keras
import matplotlib.pyplot as plt
import numpy as np


features_train = np.load('/datasets/fashion_mnist/train_features.npy')
target_train = np.load('/datasets/fashion_mnist/train_target.npy')
features_test = np.load('/datasets/fashion_mnist/test_features.npy')
target_test = np.load('/datasets/fashion_mnist/test_target.npy')

# Print feature sizes for both samples
print('Train:', features_train.shape)
print('Test:', features_test.shape)

# Print the target value for the first image from the training sample
print('First image class:', target_train[0])

# Output the image in black and white
plt.imshow(features_train[0], cmap='gray')

# Transform the dataset from a 3D array into a 2D table.
## 28 * 28 comes from the second and third value of the size
features_train = features_train.reshape(features_train.shape[0], 28 * 28)
features_test = features_test.reshape(features_test.shape[0], 28 * 28)

# Create model
model = keras.models.Sequential()

# Create layer and add the layer
model.add(
    keras.layers.Dense(units=10, input_dim=28 * 28, activation='softmax')
)

# Prepare for training
model.compile(loss='sparse_categorical_crossentropy', optimizer='sgd', metrics=['acc'])

# Train the model
model.fit(
    features_train, 
    target_train, 
    epochs=1, 
    verbose=2,
    validation_data=(features_test, target_test))
```


# Multilayer Network Training

## Understanding Multilayer Network Training
* A Multilayer Network Training project requires a lot of computational resources to train a model
	* Training typically happens in a remote server with high-powered GPUs (such as [Google Collab](https://colab.google/)).

## Process to Multilayer Network Training
* Since training a multilayer network effectively takes hours, it is best to run test code on a local computer to ensure the data loads properly and the model initiates without errors.

### Steps to Pre-Test Multilayer Network Training
1) Create a function that loads the training sample using the directory path where the data is stored.
2) Create a function that loads the test sample.
    - Extract and process the test features and target in the same way as the training set.
3) Create the model and return the model
	* Use the `input_shape=` parameter to specify the data size in the first layer
	* Don't use lengthy operations in this part of the code (test will fail)
4) Train the model
	* Train the model and return a trained model
	* The function should recieve the following as input:
		* Model
		* Training and test sets
		* Arguments for the `fit()` method
5) Run the functions
```Python

# 1) Function to load training sample 
def load_train(path):
	# Load the data 
    features_train = np.load(path + 'train_features.npy')
    target_train = np.load(path + 'train_target.npy')
	 
    # Reshape the features to they can be used by model
      # Bring the brightness of the training set images to the range of [0, 1]
    features_train = features_train.reshape(
	    features_train.shape[0], 28 * 28
	) / 255 
	
	# Return the features and targets
    return (features_train, target_train)

# 2) Function to load the test sample ()
def load_test(path):
    features_test = np.load(path + 'test_features.npy')
    target_test = np.load(path + 'test_target.npy')
    features_test = features_test.reshape(features_test.shape[0], 28 * 28) / 255.
    return (features_test, target_test)

# 3) Function to create the model
def create_model(input_shape):
	# Create the model
    model = Sequential()
    
    # Add layer(s)
    ## model.add(Dense(100, input_shape=input_shape, activation='relu'))
    ## model.add(Dense(100, activation='relu'))
    model.add(Dense(10, activation='softmax'))
    
    # Preare the model for. training
    model.compile(optimizer='sgd', loss='sparse_categorical_crossentropy',
                  metrics=['acc'])
                  
    return model

# Train the model
def train_model(model, train_data, test_data, batch_size=32, epochs=10,
    steps_per_epoch=None, validation_steps=None):
    
    # Separate out trrain and test data
    features_train, target_train = train_data
    features_test, target_test = test_data
    
    # Train the model
    model.fit(
	    features_train, target_train,
		validation_data=(features_test, target_test),
		batch_size=batch_size, 
		epochs=epochs,
		steps_per_epoch=steps_per_epoch,
		validation_steps=validation_steps,
		verbose=2, shuffle=True
	)
	
	# Return the trained model
    return model

# Run the functions (perform the test)
if __name__ == "__main__":
    train_data = load_train("/datasets/fashion_mnist/")
    test_data = load_test("/datasets/fashion_mnist/")
    model = create_model(train_data[0].shape[1:])
    model = train_model(model, train_data, test_data)
    loss, acc = model.evaluate(test_data[0], test_data[1], verbose=2)
    print("Model accuracy: {:5.2f}%".format(100 * acc))
```


# Working with Large Images
* Fully connected neural networks cannot work with large images
	* If there are not enough neurons, the network cannot find all the connections
	* If there are too many neurons, the network will overfit
* Convolution fixes the network's ability to work with large images

## Convolution
* Convolution reduces the number of neurons for each block by applying the same operation to all pixels 
	* Allows the network to learn faster and avoid overtraining
* How Convolution works:
	* The weights ($w$) move along the sequence ($s$), and the scalar product is calculated for each position on the sequence.
		* The length of the weights' vector ($n$) is never longer than the length of the sequence's vector ($m$)
		![[convolution.mp4]]
### 1D Convolution
* Formula:
	* $m$ -- the length of the vector s (sequence)
	* $n$ -- the length of the vector $w$ (weights)
	* $t$ -- the index for calculating the scalar product
	* $k$ -- any value from $0$ to ($m-n+1$) $$C_k = sum^(n-1)_(t=0)s_(k+t)w_t$$
* One-Dimensional Convolution in Python
```Python
def convolve(sequence, weights):
    convolution = np.zeros(len(sequence) - len(weights) + 1)
    for i in range(convolution.shape[0]):
        convolution[i] = np.sum(
            np.array(weights) * np.array(sequence[i : i + len(weights)])
        )
    return convolution
```

* Exercises: 
	* Question: Use the formula to calculate the result of the convolution for two sequences:
	* Solution:
		* $m = \text{length of } s$  --> 5
		* $n = \text{length of } w$ --> 2
		* Resulting vector length --> $m - n + 1 = 5 - 3 + 1 = 4$
		* Process: 
			* For $n=0$:
				* $2 * (-1) + 3 * 1 = -2 + 3 = 1$
			* For $n=1$:
				* $3*(-1) + 5*(1) = -3 + 5 = 2$
			* For $n=2$:
				* $5⋅(−1)+7⋅1=−5+7=2$
			* For $n=3$:
				* $7⋅(−1)+11⋅1=−7+11=4$
```Exercise
# Starting Values
s = [2, 3, 5, 7, 11]
w = [-1, 1]

# Answer
c = [1, 2, 2, 4]
```

### 2D Convolution
* How 2D Convolution Works:
	- The kernel traverses the image from left to right and top to bottom, multiplying its weights by by each pixel in every position.
	- The sum of these products is then recorded as the resulting pixel value.
	
- Example:
```2D Convolution
s = [[1, 1, 1, 0, 0],
     [0, 1, 1, 1, 0],
     [0, 0, 1, 1, 1],
     [0, 0, 1, 1, 0],
     [0, 1, 1, 0, 0]]

w = [[1, 0, 1],
     [0, 1, 0],
     [1, 0, 1]]
```
		![[2d-convolution-image1.png]]
		![[2d-convolution-image2.png]]
		![[2d-convolution-image3.png]]

* Formula: 
	* $t$ -- the index for calculating the scalar product
	* $k$ -- any value from $0$ to ($m-n+1$) $$C_(k_1, k_2) = sum^n_(t_1=0) * sum^n_(t_2=0) s_(k_1+t_1) w_(t_1,t_2)$$
* Example
	* $2 * (-1) + 1 * (-2) + 4*(1) + 0 *(-2) = -2 + -2 + 4 + 0 = 0$
	* $1 * (-1) + 3 * (-2) + 0 * (1) + 2*(2) = -1 + -6 + 0 + 4 = -3$
	* $4 * (-1) + 0 * (2) + 1 * (1)  + 5 * (2) = -4 + 0 + 1 + 10 = 7$
	* $0 * (-1) + 2 * (-2) + 5 * (1) + 6 * (2) = 0+ -4 + 5 + 12 = 13$
	
```Exercise
# Starting Values
s = [[2, 1, 3], 
     [4, 0, 2], 
     [1, 5, 6]]
     
 w = [[-1, -2], 
     [1,   2]]

# Answer
c = [[0, -3], [7, 13]]
```

## Convolution Layers
### What are Convolutional Layers?
- **Convolutional layers** process input images by applying a specific operation.
    - They do most of the calculations in the network.
- Each **Convolutional Layer** includes adjustable and trainable **filters** (sets of weights) that are used on the image.
    - A filter is like a square 2D grid of pixels sized ($K * K$).
        - For color images, a third dimension (depth) is added to the filter.
	- Multiple filters can exist in a convolutional layer. Each filter produces a 2D image, which can then be combined back into a 3D image.
	    - In the next convolutional layer, the depth of the filters matches the number of filters in the previous layer. 
	    
	     **Note:** *An asterisk (\*) indicates a convolution operation.*
			![[convolution-layer-multi-example.png]]
		

### How Convolution Layers Work
* Example: There are three color channels below: red, blue, and green.
	* A 3x3x3 filter (three pixels in width, height, and depth) moves through the input image in each channel, performing a convolution operation
		* It does not move through the third dimension, and each color has different weights.
	* The resulting images are folded consequently into the end-result of the convolution.
		![[convolution-layer-visual.mp4]]
* Exercise: 2x3x2 image convolution with a 2x1x2
	* Solution: 
		* $1 * (0.5) + 3 * (0.5) + 2 * (1) + 3 * (-1) = 0.5 + 1.5 + 2 - 3 = 1$
		* $3 * (0.5) + 1 * (0.5) + 2 * (1) + 2 * (-1) = 1.5 + 0.5 + 2 - 2 = 2$
		* $1 * (0.5) + 5 * (0.5) + 3 * (1) + 1 * (-1) = 0.5 + 2.5 + 3 -1 = 5$
```
# Starting Values
[[1, 3, 1]           [0.5
 [3, 1, 5]]           0.5]

[[2, 2, 3]           [1
 [3, 2, 1]]          -1]

# Result 
[1, 2, 5]
```

### How Convolutional Layers are Trained
* Convolutional layers contain fewer parameters than fully connected layers (easier to train)
	* Example: Using a 32x32x3 image
		* Convolutional Layers 
			* The size of the filter is 3x3x3. 
			* The dimensions of the output image are 30x30x1 (with just one channel). 
			* This convolutional layer has 27 parameters (3·3·3).
		* Fully Connected Layer
			* A neuron is added to each output pixel, which would require a total of 900 neurons (30·30). 
			* Each neuron is connected to every pixel of the input image, so the total number of parameters would be 2,764,800 (32·32·3·900).

### Settings for Convolutional Layers
* Padding 
	* This setting adds zeros are added around the matrix edges (zero padding). This ensures that outer pixels are involved in the convolution as often as central pixels.
		* This prevents important information from being lost. 
		* The added zeros contribute to the convolution process, and the amount of padding controls how wide the zero-padding area is.
		![[convolution-layer-setting-padding.png]]
* **Striding** (**Stride**)
	* Shifts the filter by more than one pixel and generates a smaller output image.
		![[convolution-layer-setting-stride-1.png]]
		![[convolution-layer-setting-stride-2.png]]

* Calculating Convolutional Layers with Settings
	* Convolutional Layers can be calculated using the following formula:
		* K -- Filter Size
		* $P$ -- Padding 
		* $S$ -- Stride
		* $W'$ -- New Image Size
		* $W$ -- Initial Image Size $$W' = (W - K + 2P) / S + 1$$
	* Exercise:
		* Calculate the spatial size of the output tensor for an 11x11x6 image with a 3x3x6 filter and a padding of 4 and stride of 2.
		* Solution
			* Define Function $$W' = (W-K+2P)/S + 1$$
			* Compute: $$(11 - 3 + 2(4))/2 +1 = 9$$
			* Compute: $$(11 - 3 + 2(4))/2 +1 = 9$$
			* Combine -->  _9 x 9_

### Convolutional Layers in Keras
#### The Conv2D Class
- The layers module of TensorFlow, has a `Conv2D` class (`keras.layers.Conv2D()`) which is used to create convolutional layers.
    - Parameters:
        - `filters=` -- Determines the size of the output tensor, corresponding to the number of filters.
        - `kernel_size=` -- Specifies the spatial dimensions of the filter (`K x K x D`), where `D` is the depth of the input image.
        - `strides`: Controls how the filter moves across the input matrix (default is `1`).
        - `padding=` -- Sets the width of zero padding. Two types are available:
            - `valid`: No padding (default).
            - `same`: Automatically adjusts padding so that output dimensions match input dimensions.
        - `activation=` -- Specifies the activation function applied immediately after convolution.
            - `'relu'`
            - `'sigmoid'`
        - `input_shape=` -- sets the size of the input data
* The layers module includes a class named flatten, which is used to create a layer that transforms a multidimensional tensor into a one-dimensional tensor.

#### Training a Model using Convolutional Layers
* Import the necessary modules
	* Sequential, Conv2D, Flatten, Dense
* Import the data
* Change the images dimensions and set to a range of (0, 1)
	* Can set one of the dimensions to `-1` so that it is calculated automatically
* Create the model using the Sequential class
* Add the convolutional layer using `keras.layers.Conv2D()`
* Add the `Flatten()` layer to convert the multidimensional tensor one-dimensional tensor
* Add the `Dense()` layers
* Prepare the model for training
* Train the model
```Python
# Import the modules
from tensorflow.keras import Sequential
from tensorflow.keras.layers import Conv2D, Flatten, Dense
import numpy as np

# Import data
features_train = np.load('/datasets/fashion_mnist/train_features.npy')
target_train = np.load('/datasets/fashion_mnist/train_target.npy')
features_test = np.load('/datasets/fashion_mnist/test_features.npy')
target_test = np.load('/datasets/fashion_mnist/test_target.npy')

# Change the image's dimensions and set it to a range of [0, 1].
features_train = features_train.reshape(-1, 28, 28, 1) / 255.0
features_test = features_test.reshape(-1, 28, 28, 1) / 255.0

# Create the model
model = Sequential()

# Add the convolutional layer
model.add(
    Conv2D(filters=4,
           activation="relu",
           kernel_size=(3,3), 
           input_shape=(28, 28, 1)
    )
)

# Add the Flatten layer
model.add(Flatten())

# Add the dense layer
model.add(Dense(units=10, activation='softmax'))

# Prepare the model for training
model.compile(
    loss='sparse_categorical_crossentropy', 
    optimizer='sgd', 
    metrics=['acc']
)

# Print a summary of the model
model.summary()
```

```Result -- Summary

Model: "sequential_1"
_________________________________________________________________
 Layer (type)                Output Shape              Param #
=================================================================
 conv2d_1 (Conv2D)           (None, 26, 26, 4)         40

 flatten_1 (Flatten)         (None, 2704)              0

 dense_1 (Dense)             (None, 10)                27050

=================================================================
Total params: 27,090
Trainable params: 27,090
Non-trainable params: 0
_________________________________________________________________
```

```Python
# Example -- Adding two convolutional layers 
## Two convolutional layers each with four 3x3 filters to the network. The image size remains the same after the first layer, but is decreased by half after the second layer.

from tensorflow.keras import Sequential
from tensorflow.keras.layers import Conv2D, Flatten, Dense
import numpy as np


features_train = np.load('/datasets/fashion_mnist/train_features.npy')
target_train = np.load('/datasets/fashion_mnist/train_target.npy')
features_test = np.load('/datasets/fashion_mnist/test_features.npy')
target_test = np.load('/datasets/fashion_mnist/test_target.npy')

features_train = features_train.reshape(-1, 28, 28, 1) / 255.0
features_test = features_test.reshape(-1, 28, 28, 1) / 255.0

model = Sequential()

model.add(
    Conv2D(
        filters=4,
        kernel_size=(3, 3),
        padding='same',
        activation="relu",
        input_shape=(28, 28, 1),
    )
)
model.add(
    Conv2D(
        filters=4,
        kernel_size=(3, 3),
        strides=2,
        padding='same',
        activation="relu",
    )
)

model.add(Flatten())
model.add(Dense(units=10, activation='softmax'))

model.compile(
    loss='sparse_categorical_crossentropy', optimizer='sgd', metrics=['acc']
)
model.summary()
model.fit(
    features_train,
    target_train,
    epochs=1,
    verbose=1,
    steps_per_epoch=1,
    batch_size=1,
)
```

```Result
Model: "sequential_1"
_________________________________________________________________
 Layer (type)                Output Shape              Param #
=================================================================
 conv2d_2 (Conv2D)           (None, 28, 28, 4)         40

 conv2d_3 (Conv2D)           (None, 14, 14, 4)         148

 flatten_1 (Flatten)         (None, 784)               0

 dense_1 (Dense)             (None, 10)                7850

=================================================================
Total params: 8,038
Trainable params: 8,038
Non-trainable params: 0
_________________________________________________________________

1/1 [==============================] - ETA: 0s - loss: 2.3522 - acc: 0.0000e+00
1/1 [==============================] - 0s 398ms/step - loss: 2.3522 - acc: 0.0000e+00
```


## LeNet Architecture 
### Pooling Techniques
* Pooling techniques reduce the number of the model's parameters
* Pooling Techniques:
	* Max Pooling -- returns the maximum pixel value from the pixel group within a channel. 
		* If the input image has a size of _W×W_, then the output image's size is $W/K$, where $K$ is the kernel size.
	* Average Pooling -- returns the average value of a group of pixels within a channel.
#### Max Pooling
1. The kernel size is determined (for example, 2x2)
2. The kernel starts moving left to right, top to bottom, and in each frame of pixels there is a pixel with the maximum value
3. The pixel with the maximum value remains, but the neighboring pixels disappear
4. The result is a matrix formed only from the pixels with the maximum values
	![[max-pooling-technique.png]]

#### Average Pooling
* Average pooling returns the average value of a group of pixels within a channel.
### Pooling in Keras
* The `layers`  module has a AvgPool2D and MaxPool2D class, `keras.layers.AvgPool2D()` and `keras.layers.MaxPool2D`, for creating layers that utilize Average Pooling or Max Pooling
	* Parameters
		* `pool_size=` -- Sets the pooling size. The larger it is, the more neighboring pixels are involved
		- `strides=` -- Sets a stride determines how far the filter shifts over the input matrix. If `None` is specified, the stride is equal to the pooling size
		- `padding=` -- (`'valid'`, which is 0); This parameter determines the width of the zero padding
			 - `'same'` sets the size of the padding automatically

#### Training a Model using Pooling (LeNet)
* Import the necessary modules
	* Sequential, Conv2D, Flatten, Dense, MaxPooling2D
* Import the data
* Change the images dimensions and set to a range of (0, 1)
	* Can set one of the dimensions to `-1` so that it is calculated automatically
* Create the model using the Sequential class
* Add the convolutional layer using `keras.layers.Conv2D()`
* Add the pooling layer (max pooling or average pooling, both work the same)
* Add the `Flatten()` layer to convert the multidimensional tensor one-dimensional tensor
* Add the `Dense()` layers
* Prepare the model for training
* Train the model
```Python
from tensorflow.keras import Sequential
from tensorflow.keras.layers import Conv2D, Flatten, Dense, MaxPooling2D
import matplotlib.pyplot as plt
import numpy as np


features_train = np.load('/datasets/fashion_mnist/train_features.npy')
target_train = np.load('/datasets/fashion_mnist/train_target.npy')
features_test = np.load('/datasets/fashion_mnist/test_features.npy')
target_test = np.load('/datasets/fashion_mnist/test_target.npy')

features_train = features_train.reshape(-1, 28, 28, 1) / 255.0
features_test = features_test.reshape(-1, 28, 28, 1) / 255.0

model = Sequential()
model.add(
    Conv2D(
        filters=4,
        kernel_size=(3, 3),
        padding='same',
        activation="relu",
        input_shape=(28, 28, 1),
    )
)
model.add(
    Conv2D(
        filters=4,
        kernel_size=(3, 3),
        strides=2,
        padding='same',
        activation="relu",
    )
)

# Add max pooling layer
model.add(
    MaxPooling2D(
        pool_size=(2, 2),
        strides=None,
        padding='valid'
    )
)

# Flatten the layers
model.add(Flatten())
model.add(Dense(units=10, activation='softmax'))

model.compile(
    loss='sparse_categorical_crossentropy', optimizer='sgd', metrics=['acc']
)
model.summary()
model.fit(
    features_train,
    target_train,
    epochs=1,
    verbose=1,
    steps_per_epoch=1,
    batch_size=1,
)
```

```Result
Model: "sequential"

_________________________________________________________________

 Layer (type)                Output Shape              Param #   

=================================================================

 conv2d (Conv2D)             (None, 28, 28, 4)         40        

 conv2d_1 (Conv2D)           (None, 14, 14, 4)         148       

 max_pooling2d (MaxPooling2D  (None, 7, 7, 4)          0         

 )                                                               

 flatten (Flatten)           (None, 196)               0         

 dense (Dense)               (None, 10)                1970      

=================================================================

Total params: 2,158

Trainable params: 2,158

Non-trainable params: 0

_________________________________________________________________

1/1 [==============================] - ETA: 0s - loss: 2.4439 - acc: 0.0000e+00


1/1 [==============================] - 1s 752ms/step - loss: 2.4439 - acc: 0.0000e+00
```

```Python
# Example -- Adding many layers

from tensorflow.keras import Sequential
from tensorflow.keras.layers import Conv2D, Flatten, Dense, MaxPooling2D
import matplotlib.pyplot as plt
import numpy as np


features_train = np.load('/datasets/fashion_mnist/train_features.npy')
target_train = np.load('/datasets/fashion_mnist/train_target.npy')
features_test = np.load('/datasets/fashion_mnist/test_features.npy')
target_test = np.load('/datasets/fashion_mnist/test_target.npy')

features_train = features_train.reshape(-1, 28, 28, 1) / 255.0
features_test = features_test.reshape(-1, 28, 28, 1) / 255.0

model = Sequential()
model.add(
    Conv2D(
        filters=4,
        kernel_size=(3, 3),
        padding='same',
        activation="relu",
        input_shape=(28, 28, 1),
    )
)
model.add(
    Conv2D(
        filters=4,
        kernel_size=(3, 3),
        strides=2,
        padding='same',
        activation="relu",
    )
)
model.add(
    MaxPooling2D(
        pool_size=(2, 2),
        strides=None,
        padding='valid'
    )
)

model.add(Flatten())
model.add(Dense(units=10, activation='softmax'))

model.compile(
    loss='sparse_categorical_crossentropy', optimizer='sgd', metrics=['acc']
)
model.summary()
model.fit(
    features_train,
    target_train,
    epochs=1,
    verbose=1,
    steps_per_epoch=1,
    batch_size=1,
)
```

```Result

Model: "sequential"

_________________________________________________________________

 Layer (type)                Output Shape              Param #   

=================================================================

 conv2d (Conv2D)             (None, 28, 28, 6)         156       

 average_pooling2d (AverageP  (None, 14, 14, 6)        0         

 ooling2D)                                                       

 conv2d_1 (Conv2D)           (None, 10, 10, 16)        2416      

 average_pooling2d_1 (Averag  (None, 5, 5, 16)         0         

 ePooling2D)                                                     

 flatten (Flatten)           (None, 400)               0         

 dense (Dense)               (None, 120)               48120     

 dense_1 (Dense)             (None, 84)                10164     

 dense_2 (Dense)             (None, 10)                850       

=================================================================

Total params: 61,706

Trainable params: 61,706

Non-trainable params: 0

_________________________________________________________________

1/1 [==============================] - ETA: 0s - loss: 2.2359 - acc: 0.0000e+00


1/1 [==============================] - 1s 767ms/step - loss: 2.2359 - acc: 0.0000e+00
```

## The Adam Algorithm
* Its helpful to employ any optimization algorithms that will increase computational speed and improve results.
### What is the Adam Algorithm?
* An algorithm that makes stride selection automatic by selecting different parameters for different neurons, which speeds up model training.
	* Significantly faster than the Stochastic Gradient Descent (SGD)

### The Adam Algorithm in Keras
* The TensorFlow has an `optimizers` module with an Adam class that uses the Adam Algorithm 
* Steps:
	* Import the Adam class from the optimizers module.
	* Initialize the Adam algorithm
		* The default learning rate is `0.001`; Reducing it can slow down learning, but that improves the quality of the model.
	* Pass the instance of the algorithm to the optimizer parameter of the model's compile method to prepare for training
```Python

from tensorflow.keras.optimizers import Adam
from tensorflow.keras import Sequential
from tensorflow.keras.layers import Conv2D, Flatten, Dense, MaxPooling2D
import matplotlib.pyplot as plt
import numpy as np

# Load the data
features_train = np.load('/datasets/fashion_mnist/train_features.npy')
target_train = np.load('/datasets/fashion_mnist/train_target.npy')
features_test = np.load('/datasets/fashion_mnist/test_features.npy')
target_test = np.load('/datasets/fashion_mnist/test_target.npy')

# Reshape the features
features_train = features_train.reshape(-1, 28, 28, 1) / 255.0
features_test = features_test.reshape(-1, 28, 28, 1) / 255.0

# Create the model
model = Sequential()

# Initialize the Adam algorithm
optimizer = Adam()

# Add layers to the model
model.add(
    Conv2D(
        filters=4,
        kernel_size=(3, 3),
        padding='same',
        activation="relu",
        input_shape=(28, 28, 1),
    )
)
model.add(
    Conv2D(
        filters=4,
        kernel_size=(3, 3),
        strides=2,
        padding='same',
        activation="relu",
    )
)

# Add max pooling layer
model.add(
    MaxPooling2D(
        pool_size=(2, 2),
        strides=None,
        padding='valid'
    )
)

# Flatten the layers
model.add(Flatten())
model.add(Dense(units=10, activation='softmax'))

# Prepare the model for training use the adam algorithm as the optimizer
model.compile(
    optimizer=optimizer,
    loss='sparse_categorical_crossentropy',
    metrics=['acc'],
)
```


# Working with Large Number of Images
## What are Data Generators?
* Sometimes, several folders with images need to be loaded
* Data Generators allow us to deal with huge amount of images by implementing dynamic data loading 

## Data Generators in Keras
* The TensorFlow/Keras library has a module, preprocessing, which has a ImageDataGenerator class, `keras.preprocessing.image.ImageDataGenerator()` which can be used to form batches with images and class labels based on photos in folders

### Working with Data Generators in Keras
* Import the `ImageDataGenerator()` class from the module `preprocessing`
* Create an instance of the `ImageDataGenerator()` class
	* Declare data split if needed
* Using the `flow_from_directory()` method to extract data from the folder
	* Repeat for validation data if needed
* Create model using `Sequential()` class
* Add layers as needed
* Prepare the model for training
* Train the model
	* Use the `steps_per_epoch=` to limit the number of dataset batches
```Python
# Import Library
from tensorflow.keras.preprocessing.image import ImageDataGenerator
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Conv2D, AveragePooling2D, Flatten, Dense

datagen = ImageDataGenerator(validation_split=0.25, rescale=1/255)
train_datagen_flow = datagen.flow_from_directory(
    '/datasets/fruits_small/',
    target_size=(150, 150),
    batch_size=16,
    class_mode='sparse',
    subset='training',
    seed=12345
)

val_datagen_flow = datagen.flow_from_directory(
    '/datasets/fruits_small/',
    target_size=(150, 150),
    batch_size=16,
    class_mode='sparse',
    subset='validation',
    seed=12345
)

# Find out how the class numbers relate to folder names
print(train_datagen_flow.class_indices)

# Obtain "picture-label" pairs
features, target = next(train_datagen_flow)

# Find shape of feautres
print(features.shape)

# Print pixel values 
print(features[0])


# Create model
model = Sequential()

# Add layers
model.add(
    Conv2D(
        filters=6,
        kernel_size=(3, 3),
        activation='relu',
        input_shape=(150, 150, 3),
    )
)
model.add(AveragePooling2D(pool_size=(2, 2)))
model.add(Flatten())
model.add(Dense(units=12, activation='softmax'))

# Prepare model for training
model.compile(
    loss='sparse_categorical_crossentropy', optimizer='adam', metrics=['acc']
)

# Train the model 
model.fit(
    train_datagen_flow,
    validation_data=val_datagen_flow,
    steps_per_epoch=1,
    validation_steps=1,
    verbose=2, 
    epochs=1
)
```

```Result
# Result of finding indices
{
'Banana': 0, 'Carambola': 1, 'Mango': 2, 'Orange': 3, 'Peach': 4, 'Pear': 5, 
'Persimmon': 6, 'Pitaya': 7, 'Plum': 8, 'Pomegranate': 9, 'Tomatoes': 10, 
'Muskmelon': 11
}


# The result is a four-dimensional tensor with sixteen 150x150 images with three color channels.
(16, 150, 150, 3)


# Print pixel values
[[[0.4784314  0.454902   0.454902  ]
  [0.48235297 0.50980395 0.4901961 ]
  [0.45882356 0.48627454 0.4666667 ]
  ...
  [0.21960786 0.24705884 0.2392157 ]
  [0.2627451  0.28627452 0.27450982]
  [0.30980393 0.32941177 0.32156864]]
 ...
 [[0.6862745  0.69803923 0.59607846]
  [0.7294118  0.7372549  0.63529414]
  [0.7843138  0.7843138  0.6745098 ]
  ...
  [0.0509804  0.10588236 0.07843138]
  [0.0627451  0.11764707 0.09019608]
  [0.0627451  0.11764707 0.09019608]]]


Found 1266 images belonging to 12 classes.
Found 417 images belonging to 12 classes.
1/1 - 2s - loss: 236.1394 - acc: 0.0625 - val_loss: 934.5588 - val_acc: 0.0625 - 2s/epoch - 2s/step
```

## Image Data Augmentations
* If there are too few training samples, the network may overtrain
	* Augmentation can be used to help solve this issue

### What is Augmentation?
* Augmentation -- artificially expand a dataset by transforming existing images.
	* The changes are only applied to training sets.
	* Test and validation sets remain the same.
* Augmentation transforms the original image while still preserving its core features.
	* For example, image can be rotated or scaled
* Augmentations can cause problems
	* For example, the image class can change, or the end result might end up resembling an impressionist painting because of all the alterations.

### Types of Augmentations
* There are several types of augmentations:
	* Rotation of the images
	* Scaling the images
	* Changing brightness and contrast
	* Stretching and compressing
	* Blurring and sharpening
	* Adding noise

### Avoiding Problems in Augmentations
* Problems can be avoided:
	* Do not apply augmentation on test and validation sets so as not to distort metric values.
	* Add augmentations gradually, one at a time, and keep an eye on the quality metric in the validation set.
	* Always leave some images in the dataset unchanged.

### Augmentations in Keras
* Image augmentations can be added in the ImageDataGenerator class using parameters but are disabled by default.
	* Here are the parameters:
		* `horizontal_flip=`
		* `vertical_flip=`
		* `rotation_range=`
		* `width_shift_range=`
		* `height_shift_range=`
```Python
# Apply vertical flip
datagen = ImageDataGenerator(
	 validation_split=0.25, 
	 rescale=1./255, 
	 vertical_flip=True
)
```

* Steps for augmentations
	* Import libraries and modules
	* Create instance(s) of the `ImageDataGenerator()`
		* Create different generators have to be created for the training and validation sets
		* Set the objects datagen objects of the train and validation sets to the same `seed=` value to prevent the training and validation sets from sharing common elements.
	* 
```Python
# Full Example -- Using augmentations

# Import modules and libraries
from tensorflow.keras.preprocessing.image import ImageDataGenerator
import matplotlib.pyplot as plt
 
# Create two generators instead of one: train_datagen and valid_datagen
## Apply augmentations to train_datagen
train_datagen = ImageDataGenerator(
    validation_split=0.25, 
    rescale=1/255, 
    horizontal_flip=True, 
    vertical_flip=True,
    rotation_range=90,
    width_shift_range=0.20,
    height_shift_range=0.20,
)

validation_datagen = ImageDataGenerator(
    validation_split=0.25,
    rescale=1./255
)

train_datagen_flow = train_datagen.flow_from_directory(
    '/datasets/fruits_small/',
    target_size=(150, 150),
    batch_size=16,
    class_mode='sparse',
    subset='training',
    seed=12345)

val_datagen_flow = validation_datagen.flow_from_directory(
    '/datasets/fruits_small/',
    target_size=(150, 150),
    batch_size=16,
    class_mode='sparse',
    subset='validation',
    seed=12345)


# Extract features
features, target = next(train_datagen_flow)

# Display 16 images
fig = plt.figure(figsize=(10,10))
for i in range(16):
    fig.add_subplot(4, 4, i+1)
    plt.imshow(features[i])
	# remove axes & place the images closer to one another for a compact output
    plt.xticks([])
    plt.yticks([])
    plt.tight_layout()
```

