See:
* [[Py - Introduction to Python]]
* [[DS - What is Data Science?]]
* [[Py - Sklearn (SciKit Learn Library)]]
Resources
* Documentation: [SK-Learn](https://scikit-learn.org/stable/)
* Article: [Supervised vs Unsupervised Learning](https://cloud.google.com/discover/supervised-vs-unsupervised-learning#:~:text=The%20difference%20between%20supervised%20and%20unsupervised%20learning,-The%20biggest%20difference&text=Supervised%20learning%20uses%20labeled%20training,correct%20output%20values%20should%20be.)
* Article: [Model Fit: Underfitting vs Overfitting](https://docs.aws.amazon.com/machine-learning/latest/dg/model-fit-underfitting-vs-overfitting.html)
* Article: [Overfitting vs. Underfitting: What’s the Difference?](https://www.coursera.org/articles/overfitting-vs-underfitting)

---
# What is Machine Learning?
* **Machine learning (ML)** -- a tool for creating software from datasets from data
* ML models can produce automated insights from data and improve without being explicitly programmed

# Categories of Machine Learning Models
### Supervised Learning
* Features
	* Uses labeled training data
	* The target feature is known
* Types of Supervised Learning
	* **Classification** -- tasks that deal with categorical targets
		* Example(s):
			* Determining animal species in a picture
	* **Binary Classification** -- tasks that deal with categorical targets (when only two categories are possible)
		* Example(s):
			* Determining whether a client is coming back to the site or not
	* **Regression** -- tasks that deal with finding relationships between variables and make predictions based on the information
		* Example(s)
			* Weather forecasting or predicting stock market prices for upcoming days
### Unsupervised Learning
* Features
	* Does not use labeled training data 
	* The target feature is not known
### Semi-Supervised Learning
* Features
	* Target is only known for a portion of the training data
### Recommendation
* Features
	* Users and items replace features and observations


---
## Dataset Terminology
* Rows -- represent observations
* Columns -- represent features
		![[ml-obersations-features.png]]


---
---
# Features & Target

### Target
* **Target** (answer) -- the feature in the dataset that we want to understand more clearly; it is the variable the will be predicted using the rest of the dataset
	* Target can be numerical or categorical.
		* If it is categorical than the task is categorical 
		* If it is numerical than the task is regression

### Features
* Features -- the columns that are used to help predict or provide an answer to the target
	* Does not include the target feature

---
# Models and Algorithms 

## Machine Learning Process
1. Analyze relationships between features & the target variable in a dataset (Training Dataset)
2. Make assumptions and predictions on the relationships for **modeling**
	* Modeling --- process where machine learning models are developed using assumptions and prediction techniques.
3. Develop a Learning Algorithm to train the model & produce a trained model
	* Learning Algorithms -- uses a training dataset to train the model and to produce a trained model
4. Use the trained model to make predictions 
	* Take new features as input and output answers (the target) without the need for learning algorithms and training datasets
	![[learning-algorithm.png]]
	
	**Machine Learning FlowChart:**
	* The training dataset is stored in `features` and `target` variables.
	* The features of the new observations are recorded in the `new_features` variable. Now we need to find the target.
	* The `fit()` method is used for training, and the `predict()` method is used for testing.
	* The model is stored in the model variable. After it is done training, it can be used for prediction.
	![[model-training-and-model-application.png]]


---
# Parameters and Hyperparameters
**Parameters**:
* Internal variables whose values are learned from the training data during the model training process
* Directly contribute to making predictions by the model

**Hyperparameters**:
- External to the model
- Set prior to training
- Control the overall behavior of the model and affect the learning process




---
# What is Underfitting and Overfitting?

## Overfitting
* Overfitting -- a model performs well on the training data but does not perform well on the test data
## Underfitting
* Underfitting -- a model performs poorly on both training and test data.
* Why does Underfitting occur?
	* Underfitting occurs when a model is too simplistic to capture or learn the underlying patterns in the training data.

## Underfitting and Overfitting Graphical View
![[underfitting-overfitting-graphs.png]]

## Tree Depth: Overfitting and Underfitting
* How does depth impact overfitting and underfitting?
	* A high tree depth means the model tends towards overfitting
	* A short tree can lead to underfitting
* The tree-depth can be manually set when creating the model 
![[tree-overfitting-underfitting.png]]

## Real-World Comparison: Overfitting vs Underfitting
* Overfitting
	* Studying too hard for a test, where you memorize the entire textbook word for word, but focus too much on textbook material. Then we you take a test, and encounter a question that was in the textbook, you don't know how to answer it
* Underfitting
	* Not having enough time to read through all the study material, let alone memorize any answers

---
# Simple ML Workflow
1) Import the data
	* Split the data as needed (2:1 or 3:1:1)
2) Prepare the data, features and targets
	* Train different models with train data
	* Validate the different models with the validation data
	* Find the accuracy of the model with the validation data
3) Declare a final model
	* Train the final model
	* Test the final model with the test data
4) Count / calculate the number of errors from the Test data
	* Count the number of errors 
	* Calculate the accuracy