See:
* [[Py - Introduction to Python]]
* [[Py - Keras (Basics)]]
* [[Py - TensorFlow (Basics)]]
* [[Py - ML (Computer Vision)]]
Resources:
* Documentation: [Keras](https://keras.io/getting_started/)
* Documentation: [TensorFlow](https://www.tensorflow.org/tutorials)


---
# Classes

##### `keras.models.Sequential()`
* Groups a linear stack of layers into a Model.
	* Parameters
		* `layers=`
		* `trainable=` (bool) -- (`True`)
		* `name=` 
	* Methods (see complete list of methods [here](https://www.tensorflow.org/api_docs/python/tf/keras/Sequential))
		* `add()` -- Adds a layer instance on top of the layer stack.
			* `layer` -- The layer to add 
			* `rebuild=` (bool) -- (`True`)
		* `compile()` -- Configures the model for training.
			* `optimizer=` (str) -- name of optimizer or optimizer instance
			* `loss=` (str) -- Name of the loss function to use
			* `loss_weights=` (list / dict) -- List or dict specifying scalar coefficients (Python floats) to weight the loss contributions of different model outputs.
			* `metrics=` (list) -- List of metrics to be evaluated by the model during training and testing
		* `fit()` -- Trains the model for a fixed number of epochs (dataset iterations)
			* `x` (array, tensor dict) -- the input features
			* `y` (array, tensor dict) -- the target target
			* `batch_size=` (int or None) -- (`None`); Number of samples per gradient update.
			* `epochs=` (int) -- (`1`); Number of epochs to train the model. 
				* An epoch is an iteration over the entire `x` and `y` data provided.
			*  `verbose=` (str) -- (`'auto'`); `"auto"`, 0, 1, or 2. Sets the verbosity mode. 
				* 0 = silent
				* 1 = progress bar
				* 2 = one line per epoch
				* "auto" becomes 1 for most cases
			* `validation_data=` (tuple) -- (`None`); Data on which to evaluate the loss and any model metrics at the end of each epoch. The model will not be trained on this data.
		* `summary()` -- Prints a summary of the model
```Python
# Import Keras
from tensorflow import keras

# Create the model
model = keras.models.Sequential()

model.add(keras.layers.Dense(
	 units=1, 
	 input_dim=features_train.shape[1])
)

model.compile(loss='mean_squared_error', optimizer='sgd')
```

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

model.add(
    keras.layers.Dense(
        units=1, input_dim=features_train.shape[1], activation='sigmoid'
    )
)

model.compile(loss='binary_crossentropy', optimizer='sgd', metrics=['acc'])

model.fit(features_train, target_train, epochs=10, verbose=2,
          validation_data=(features_valid, target_valid))
```

##### `keras.layers.Dense()`
* Creates a regular densely-connected NN layer.
	* Parameters (see full list of parameters [here](https://www.tensorflow.org/api_docs/python/tf/keras/layers/Dense))
		* `units=` (int) -- Sets dimensionality of the output space.
		* `activation=` (str) -- (`'linear'`); Sets the activation function to use
		* `input_dim=` (int) -- Sets the number of inputs in the layer
```Python
keras.layers.Dense(units=1, input_dim=features.shape[1])
```

##### `keras.layers.Conv2D()`
* Creates a 2D convolution layer.
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
```Python
# Example -- Using a convolutional layer in keras

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


##### `keras.layers.AvgPool2D()`
* Average pooling operation for 2D spatial data.
	* Parameters
		* `pool_size=` -- Sets the pooling size. The larger it is, the more neighboring pixels are involved
		- `strides=` -- Sets a stride determines how far the filter shifts over the input matrix. If `None` is specified, the stride is equal to the pooling size
		- `padding=` -- (`'valid'`, which is 0); This parameter determines the width of the zero padding
			 - `'same'` sets the size of the padding automatically
```Python
from tensorflow.keras import Sequential
from tensorflow.keras.layers import Conv2D, Flatten, Dense, AvgPool2D
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
        filters=6,
        kernel_size=(5, 5),
        padding='same',
        activation="tanh",
        input_shape=(28, 28, 1),
    )
)
model.add(
    AvgPool2D(
        pool_size=(2, 2),
        padding='valid',
        strides=None,
    )
)

model.add(Flatten())

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

##### `keras.layers.MaxPool2D()`
* Max pooling operation for 2D spatial data.
	* Parameters
		* `pool_size=` -- Sets the pooling size. The larger it is, the more neighboring pixels are involved
		- `strides=` -- Sets a stride determines how far the filter shifts over the input matrix. If `None` is specified, the stride is equal to the pooling size
		- `padding=` -- (`'valid'`, which is 0); This parameter determines the width of the zero padding
			 - `'same'` sets the size of the padding automatically
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


##### `keras.optimizers.Adam()`
* Optimizer that implements the Adam algorithm
	* Parameters
		* `learning_rate=` (float) -- (`0.001`); Sets the learning rate for the optimizer 
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

##### `keras.preprocessing.image.ImageDataGenerator()`
* Forms batches with images and class labels based on the photos in the folders
	* Parameters
		* `validation_split=` (float) -- An optional float between 0 and 1, fraction of data to reserve for validation.
		* `rescale` -- Fits the data generator to some sample data.
		* `horizontal_flip=` (bool) -- (`False`); Flips the image on horizontal axis
		* `vertical_flip=` (bool) -- (`False`); Flips the image on vertical axis
		* `rotation_range=` (int) -- (`False`); Rotates the image by specified degree
		* `width_shift_range=` (float) -- (`False`); A number between 0 and 1 that represents the fraction of the total width of the image by which the image can be horizontally shifted.
		* `height_shift_range=` (float) -- (`False`); A number between 0 and 1 that represents the fraction of the total width of the image by which the image can be vertically shifted.
	* Methods
		* `flow_from_directory()`
			* Extracts data from a folder and returns an object
			* Parameters
				* `directory` (str) -- the pathway to the folder
				* `target_size=` (tuple) -- the target size (width and height) of the image. This will set all images to the same target size (needed for neural network)
				* `batch_size=` (int) -- the number of images in the batches. The more images there are, the more effective the model's training will be.
					* Too many won't fit the GPU's memory (16 is a good sweet spot)
				* `class_mode=` (str) -- the class mode to be used
					* `'sparse'` -- the labels will correspond to the number of the folder.
				* `subset=` -- The subset of data that the result belongs to
					* `'training'`
					* `'validation'`
				* `seed=` (int) -- sets a random number generator
	* Properties
		* `class_indices` -- Displays how the class numbers relate to the folder names
```Python
from tensorflow.keras.preprocessing.image import ImageDataGenerator

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

print(train_datagen_flow.class_indices)
```

```Result
{
'Banana': 0, 'Carambola': 1, 'Mango': 2, 'Orange': 3, 'Peach': 4, 'Pear': 5, 
'Persimmon': 6, 'Pitaya': 7, 'Plum': 8, 'Pomegranate': 9, 'Tomatoes': 10, 
'Muskmelon': 11
}
```

```Python
# Import modules and libraries
from tensorflow.keras.preprocessing.image import ImageDataGenerator
 
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

```


##### `keras.applications.resnet.ResNet50()`
* Instantiates the ResNet50 architecture
	* Parameters
		* `input_shape=` (tuple) -- a tuple that specifies the size of the input image.
		* `classes=` (int) -- the number of neurons in the last fully connected layer where classification takes place.
		* `weights=` (str) -- sets the initialization of weights
			* `None` -- (random initialization); randomly initiates weights
			* `"imagenet"` -- (pre-training on ImageNet); ImageNet is the name of a large image database which was used to train the network to sort pictures into 1000 classes.
		* `include_top=` (bool) -- specifies whether or not to include a fully-connected layer (_GlobalAveragePooling2D_ and _Dense_) at the top of the network
```Python
from tensorflow.keras.applications.resnet import ResNet50

model = ResNet50(
	input_shape=None,
	classes=1000,
	include_top=True,
	weights='imagenet'
)
```
