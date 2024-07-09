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

#### `keras.models.Sequential()`
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

#### `keras.layers.Dense()`
* Creates a regular densely-connected NN layer.
	* Parameters (see full list of parameters [here](https://www.tensorflow.org/api_docs/python/tf/keras/layers/Dense))
		* `units=` (int) -- Sets dimensionality of the output space.
		* `activation=` (str) -- (`'linear'`); Sets the activation function to use
		* `input_dim=` (int) -- Sets the number of inputs in the layer
```Python
keras.layers.Dense(units=1, input_dim=features.shape[1])
```