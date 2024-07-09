See:
* [[Py - Introduction to Python]]
* [[Py - Pandas (Basics)]]

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

