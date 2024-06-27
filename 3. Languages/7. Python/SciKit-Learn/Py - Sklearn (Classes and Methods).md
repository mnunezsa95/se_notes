See:
* [[Py - Introduction to Python]]
* [[ML - Machine Learning Basics]]
* [[Py - Sklearn (Models & Model Comparison)]]
* [[ML - Supervised Learning]]]]
Resources
* Documentation: [SK-Learn](https://scikit-learn.org/stable/)

---

# Classes

##### `sklearn.feature_extraction.text.CountVectorizier()`
* Converts a collection of text documents to a matrix of token counts.
	* Parameters (see complete parameters in [documentation](https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.CountVectorizer.html))
		* `input` (str) -- (`'content'`); 
			* If `'filename'`, the sequence passed as an argument to fit is expected to be a list of filenames that need reading to fetch the raw content to analyze.
			* If `'file'`, the sequence items must have a ‘read’ method (file-like object) that is called to fetch the bytes in memory.
			* If `'content'`, the input is expected to be a sequence of items that can be of type string or byte.
		* `enocding` (str) --  (`'utf-8'`); Specifies the encoding used to decode If bytes or files are given to analyze
		* `decode_error` (str) -- (`'strict'`); Instruction on what to do if a byte sequence is given to analyze that contains characters not of the given `encoding`.
		* `lowercase=` (bool) -- (`True`); Convert all characters to lowercase before tokenizing.
		* `ngram_range=` (tuple) -- Specifies the min and max n-gram values to use when calculating n-gram count
			* The lower and upper boundary of the range of n-values for different word n-grams or char n-grams to be extracted. All values of n such such that min_n <= n <= max_n will be used
		* `stop_words=` (list) -- (`None`); Removes the specified stop words from the text;
			* If a list, that list is assumed to contain stop words, all of which will be removed from the resulting tokens
			* If `'english'`, a built-in stop word list for English is used. There are several known issues with ‘english’ and you should consider an alternative
	* Methods
		* `fit_transform()` -- Learns the vocabulary dictionary and returns a matrix, where rows represent texts, and the columns display unique words from the corpus
			* `raw_documents` (iterable) -- An iterable which generates either str, unicode or file objects.
		* `fit()` -- Learns a vocabulary dictionary of all tokens in the raw documents.
		* `raw_documents` (iterable) -- An iterable which generates either str, unicode or file objects.
		* `get_feature_names_out()` -- Get output feature names for transformation.
			* `input_features=` (str); Not used, present for API consistency by convention.
	* Attributes
		* `shape` -- Returns the shape of the model
```Python
# Creating a bag-of-words

# Import Class
from sklearn.feature_extraction.text import CountVectorizer

# Create an instance of the class
count_vect = CountVectorizer()

# Fit the model to the dataset
bow = count_vect.fit_transform(corpus)

# Get list of features
count_vect.get_feature_names()
```

```Python
# Calculating n-grams

# Import Class
import pandas as pd
from sklearn.feature_extraction.text import CountVectorizer

data = pd.read_csv('/datasets/imdb_reviews_small_lemm.tsv', sep='\t')

# The corpus 
corpus = data['review_lemm']

# Create an instance of the class & specify the max and min ngram_range
count_vect = CountVectorizer(ngram_range=(2,2))
n_gram = count_vect.fit_transform(corpus)

print('The size of 2-gram:', n_gram.shape)
```


##### `sklearn.feature_extraction.text.TfidfVectorizer()`
* Convert a collection of raw documents to a matrix of TF-IDF features.
	* Parameters (see complete parameters in [documentation](https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.TfidfVectorizer.html))
		* `input` (str) -- (`'content'`); 
			* If `'filename'`, the sequence passed as an argument to fit is expected to be a list of filenames that need reading to fetch the raw content to analyze.
			* If `'file'`, the sequence items must have a ‘read’ method (file-like object) that is called to fetch the bytes in memory.
			* If `'content'`, the input is expected to be a sequence of items that can be of type string or byte.
		* `enocding` (str) --  (`'utf-8'`); Specifies the encoding used to decode If bytes or files are given to analyze
		* `decode_error` (str) -- (`'strict'`); Instruction on what to do if a byte sequence is given to analyze that contains characters not of the given `encoding`.
		* `lowercase=` (bool) -- (`True`); Convert all characters to lowercase before tokenizing.
		* `ngram_range=` (tuple) -- Specifies the min and max n-gram values to use when calculating n-gram count
			* The lower and upper boundary of the range of n-values for different word n-grams or char n-grams to be extracted. All values of n such such that min_n <= n <= max_n will be used
		* `stop_words=` (list) -- (`None`); Removes the specified stop words from the text;
			* If a list, that list is assumed to contain stop words, all of which will be removed from the resulting tokens
			* If `'english'`, a built-in stop word list for English is used. There are several known issues with ‘english’ and you should consider an alternative
	* Methods
		* `fit_transform()` -- Learns the vocabulary dictionary and returns a matrix, where rows represent texts, and the columns display unique words from the corpus
			* `raw_documents` (iterable) -- An iterable which generates either str, unicode or file objects
		* `fit()` -- Learns the vocabulary and idf from training set.
			* `raw_documents` (iterable) -- An iterable which generates either str, unicode or file objects
		* `get_feature_names_out()` -- Get output feature names for transformation.
			* `input_features=` (str); Not used, present for API consistency by convention.
	* Attributes
		* `shape` -- Returns the shape of the model
```Python
# Full Example

# Import libraries
import pandas as pd
from nltk.corpus import stopwords as nltk_stopwords
from sklearn.feature_extraction.text import TfidfVectorizer

# Load data
data = pd.read_csv('/datasets/imdb_reviews_small_lemm.tsv', sep='\t')

# Define corpus
corpus = data['review_lemm']

# Define stop words
stop_words = set(nltk_stopwords.words('english'))

# Create instance
count_tf_idf = TfidfVectorizer(stop_words=stop_words)

# Fit the counter instance
tf_idf = count_tf_idf.fit_transform(corpus)

print('The TF-IDF matrix size:', tf_idf.shape) # The TF-IDF matrix size: (4541, 26098)
```

# Methods
