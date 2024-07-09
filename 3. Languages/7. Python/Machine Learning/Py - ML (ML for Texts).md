See:
* [[Py - Introduction to Python]]
* [[Py - Pandas (Basics)]]
* [[Py - Pandas (Working with Pandas)]]
* [[Py - Pandas (Methods)]]
* [[Py - Regular Expressions (Basics)]]
* [[Py - NLTK (Basics)]]
* [[Py - NLTK (Methods)]]
* [[Py - spaCy (Basics)]]
* [[Py - spaCy (Methods)]]
* [[Py - PyTorch (Basics)]]
* [[Py - Transformers (Basics)]]
* [[Py - Transformers (Methods)]]
Resources:
* TripleTen Knowledge Base: [Data Science](https://tripleten.netlify.app/)
* Documentation: [Pandas](https://pandas.pydata.org/docs/)
* Documentation: [NumPy](https://numpy.org/doc/stable/index.html)
* Documentation: [SK-Learn](https://scikit-learn.org/stable/)
* Documentation: [SciPy](https://docs.scipy.org/doc/scipy/index.html)
* Documentation: [NLTK](https://www.nltk.org/)
* Documentation: [spaCy](https://spacy.io/)
* Documentation: [spaCy Models](https://spacy.io/models/en)
* Documentation: [PyTorch](https://pytorch.org/docs/stable/index.html)
* Documentation: [transformers](https://huggingface.co/docs/transformers/en/index)
* GitHub: [Gensim](https://github.com/piskvorky/gensim-data)

---
# ML for Text (Verbiage)
- NLP = Natural Language Processing
- Corpus -- A collection of texts
- Text record -- A single text entry

# Lemmatization
## Working with Words
* Before words can be used to create features, it MUST be simplified via two processes.
* Here are the steps for text preprocessing:
	1. **Tokenization:** Divides the text into tokens (separate phrases, words, and symbols);
	2. **Lemmatization:** Reduces the words to their root forms (lemma).

## Libraries for Tokenization & Lemmatization
* Popular libraries for both tokenization and lemmatization:
	- Natural Language Toolkit (NLTK)
	- spaCy
	- UDPipe
	- word2vec 

## Tokenizing and Lemmatizing Words (NLTK)
* The NLTK Library has classes and functions for working with words
	* The `nltk.stem.WordNetLemmatizer()` class Lemmatizes a word using WordNet’s built-in morphy function
		* Word(s) passed into this object must be in lowercase!
	* The `nltk.tokenize.word_tokenize()` method returns a tokenized copy of _text_, using NLTK’s recommended word tokenizer
```Python
# Import Libraries
from nltk.tokenize import word_tokenize
from nltk.stem import WordNetLemmatizer

# Create a Lemmatizer Object
lemmatizer  = WordNetLemmatizer()

# Creating a tokenized copy of the text
text = "All models are wrong, but some are useful." 
tokens = word_tokenize(text.lower())

# Passing in each 'token' into lemmatize
lemmas = [lemmatizer.lemmatize(token) for token in tokens]
print(lemmas)

# Joining the lemmas together into a string
lemmas_joined = "".join(lemmas)
print(lemmas_joined)
```

```Result
['all', 'model', 'are', 'wrong', ',', 'but', 'some', 'are', 'useful', '.']

'all model are wrong , but some are useful .'
```

## Tokenizing and Lemmatizing Words (spaCy)
* The spaCy Library has classes and functions for working with words
	* The `spacy.load()` method loads the small-size English-language model and disable some components of the pipeline
	* The `token.lemma_` attribute has the results assigned to it
```Python
# Import Library
import spacy

# Loads the small-size English-language model and disable some components of the pipeline
nlp = spacy.load('en_core_web_sm', disable=['parser', 'ner'])

# Lowercase every word
doc = nlp(text.lower())

# Create a list containing the lemmatized words
lemmas = [token.lemma_ for token in doc]
print(lemmas)

# Joining the lemmas together into a string
lemmas_joined = " ".join(lemmas)
print(lemmas_joined)
```

```Result
['all', 'model', 'are', 'wrong', ',', 'but', 'some', 'are', 'useful', '.']

all model be wrong , but some be useful .
```

```Python
import pandas as pd
import random
import spacy

nlp = spacy.load('en_core_web_sm', disable=['parser', 'ner'])

data = pd.read_csv('/datasets/imdb_reviews_small.tsv', sep='\t')
corpus = data['review']


def lemmatize(text):
    doc = nlp(text.lower())
    lemmas = [token.lemma_ for token in doc]
    return " ".join(lemmas)

review_idx = random.randint(0, len(corpus) - 1)
review = corpus[review_idx]

print('The original text:', review)
print()
print('The lemmatized text:', lemmatize(review))
```

```Result
The original text: After Racism, Rural exodus -also known as migration from the country side- is another socio-political issue of the 1960s. WestSide Story had dealt with Racism by a love feast in an artistic view. Now, Midnight Cowboy deals with rural exodus by a friendship tragedy in a psychological view. It has a deeply grievous ending that we witness one of the two companions of fate passing away. Director John Schlesinger skillfully deliver us the deepest secret thoughts, dreams, fantasies, fears and evaluations of two New York City scums. ...

The lemmatized text: after racism , rural exodus -also know as migration from the country side- be another socio - political issue of the 1960 . westside story have deal with racism by a love feast in an artistic view . now , midnight cowboy deal with rural exodus by a friendship tragedy in a psychological view . it have a deeply grievous ending that we witness one of the two companion of fate pass away . director john schlesinger skillfully deliver we the deep secret thought , dream , fantasy , fear and evaluation of two new york city scums . 
...
```

# Text Pre-Processing using Regular Expressions
## When are Regular Expressions useful in ML for Texts?
* Regular expressions find sequences of characters, words, and numbers by pattern recognition.
* In ML for texts, Regular Expressions can be used to clean the text BEFORE being lemmatized

## Text Pre-Processings Steps
1) Regular Expressions can be used to remove all characters except letters, apostrophes, and spaces from text
```Python
# This RegEx will find characters that DON'T match the following:
## 1) any character a-z
## 2) any character A-Z, 
## 3) an apostrophe
pattern = r"[^a-zA-Z']"
text = re.sub(pattern, " ", text)
print(text)
```

```Result 
# Before
I liked this show from the first episode I saw, which was the "Rhapsody in Blue" episode (for those that don't know what that is, the Zan going insane and becoming pau lvl 10 ep). Best visuals and special effects I've seen on a television series, nothing like it anywhere.

# After
" I liked this show from the first episode I saw  which was the  Rhapsody in Blue  episode  for those that don't know what that is  the Zan going insane and becoming pau lvl    ep   Best visuals and special effects I've seen on a television series  nothing like it anywhere  "
```
2) The `split()` and `join()` methods can be used to remove additional spaces
```Python
text = text.split()
text = " ".join(text)
```

```Result
# After
"I liked this show from the first episode I saw which was the Rhapsody in Blue episode for those that don't know what that is the Zan going insane and becoming pau lvl ep Best visuals and special effects I've seen on a television series nothing like it anywhere"

```

```Python
# Full Example

import random 
import pandas as pd
import re
import spacy

nlp = spacy.load('en_core_web_sm', disable=['parser', 'ner'])

data = pd.read_csv('/datasets/imdb_reviews_small.tsv', sep='\t')
corpus = data['review']

def clear_text(text):
    pattern = r"[^A-Za-z']"
    clean_text = re.sub(pattern, " ", text)
    clean_text = " ".join(clean_text.split())
    return clean_text

def lemmatize(text):
    doc = nlp(text.lower())
    lemmas = []
    for token in doc:
        lemmas.append(token.lemma_)
    return ' '.join(lemmas)

review_idx = random.randint(0, len(corpus)-1)
review = corpus[review_idx]

print('The original text:', review)
print()
print('The lemmatized text:', lemmatize(clear_text(review)))
```

# Bag-of-Words and N-Gram
## Introduction
- Numeric data is more suitable for computer processing.
- Text data must be converted into numerical form.
    - Typically, words or sentences are transformed into numerical vectors.

## The Bag-of-Words Model
* Bag-of-Words Model -- A method for text conversion
- Converts texts into vectors without accounting for word order
    - Counts each unique word while ignoring the sequence and relationships between words
- The Bag-of-Words approach transforms multiple texts into a matrix form:
    - **Rows**: Each row represents a different text.
    - **Columns**: Each column denotes a unique word from the complete set of texts (corpus).
```Example
# Text
For want of a nail the shoe was lost.
For want of a shoe the horse was lost.
For want of a horse the rider was lost.

# Get rid of uppercase letters and lemmatize it with spaCy
for want of a nail the shoe be lose 
for want of a shoe the horse be lose 
for want of a horse the rider be lose

# Result --> The number of times each word occurs
[3, 3, 3, 2, 3, 1, 3, 1, 2, 3, 3]

- "for," "want," "of," "a," "the," "be," "lose" — 3;
- "shoe," "horse" — 2;
- "nail," "rider" — 1.
```

### Creating a Bag-of-Words
* Sklearn has a `CountVectorizier()` class in the `sklearn.feature_extraction.text` module used to create a bag-of-words
* Steps
	1. Import the `stopwords` package from the `nltk.corpus` module.
	2. Import the `nltk` library.
	3. Download the necessary package using the `nltk.download()` method.
	4. Use the `stopwords.words()` function with the argument `english` to obtain the English stop words and store them in a variable.
	5. Import the `CountVectorizer` class.
	6. Instantiate the `CountVectorizer` class, passing the stop words variable to the `stop_words` parameter.
	7. Fit the model using the `fit_transform()` method and assign the result to a variable `bow`. This method returns a matrix where each row represents a text, and each column corresponds to a unique word from the corpus.
	8. Check the shape of the `bow` model using its `shape` attribute.
	9. Convert the `bow` matrix to an array using the `toarray()` method.
	10. Retrieve the vocabulary (list of unique words) with the `get_feature_names_out()` method.
```Python
# Imports 
from sklearn.feature_extraction.text import CountVectorizer
from nltk.corpus import stopwords
import nltk

# Download the package
nltk.download('stopwords')

# Get a set of stop words for English
stop_words = set(stopwords.words('english'))

# Create an instance of the class and pass in the stop words
count_vect = CountVectorizer(stop_words=stop_words)

# The corpus
corpus = [
    'for want of a nail the shoe be lose',
    'for want of a shoe the horse be lose',
    'for want of a horse the rider be lose',
    'for want of a rider the message be lose',
    'for want of a message the battle be lose',
    'for want of a battle the kingdom be lose',
    'and all for the want of a horseshoe nail'
]

# Fit the model to the dataset
bow = count_vect.fit_transform(corpus)

# Find the shape of the model
bow.shape # (7, 16) The result is 7 texts and 16 unique words.

# Create an array from the matrix
print(bow.toarray())

# Get list of feature names
count_vect.get_feature_names_out()
```

```Result
[[0 0 0 1 0 0 0 1 0 1 1 0 1 1 1 1]
 [0 0 0 1 1 0 0 1 0 0 1 0 1 1 1 1]
 [0 0 0 1 1 0 0 1 0 0 1 1 0 1 1 1]
 [0 0 0 1 0 0 0 1 1 0 1 1 0 1 1 1]
 [0 0 1 1 0 0 0 1 1 0 1 0 0 1 1 1]
 [0 0 1 1 0 0 1 1 0 0 1 0 0 1 1 1]
 [1 1 0 1 0 1 0 0 0 1 1 0 0 1 1 0]]

['battle', 'horse', 'horseshoe', 'kingdom', 'lose', 'message', 'nail', 'rider', 'shoe', 'want']
```

```Python
# Example - Creating bag-of-words with and without stop words

import pandas as pd
from sklearn.feature_extraction.text import CountVectorizer
from nltk.corpus import stopwords
import nltk

data = pd.read_csv('/datasets/imdb_reviews_small_lemm.tsv', sep='\t')
corpus = data['review_lemm']

# ============= Creating bag-of-words WITH stop words ============= #
count_vect = CountVectorizer()
bow = count_vect.fit_transform(corpus)

print('The BoW size with stop words:', bow.shape) # The BoW size with stop words: (4541, 26214)

# ============= Creating bag-of-words WITHOUT stop words ============= #

nltk.download('stopwrds')
stop_words = set(stopwords.words('english'))
count_vect = CountVectorizer(stop_words=stop_words)
bow = count_vect.fit_transform(corpus)

print('The BoW size without stop words:', bow.shape) # The BoW size without stop words: (4541, 26098)
```


## N-Grams
* N-Gram -- a sequence of several words
	* $N$ -- indicates the number of elements and is arbitrary
		* If $N=1$  -- separate words or **unigrams**. 
		* If $N=2$ -- two-word phrases or **bigrams**. 
		* If $N=3$  -- three-word phrases or **trigrams**
		* etc
* Example: Number of Trigrams in the phrase 'Sunset raged like a beautiful bonfire'
![[n-gram-visual.png]]\
* Question: How many bigrams can we get from this text? ''It is happening. Bird has landed. Get going.''
	* Answer: 5
		* It is
		* is happening
		* Bird has
		* has landed
		* Get going

### Calculating N-Grams
* Sklearn has a `CountVectorizier()` class in the `sklearn.feature_extraction.text` module used for n-gram calculations
* Steps
	- Import the class.
	- Instantiate the class and define the n-gram size using the `ngram_range=` parameter to count the phrases.
	    - This parameter accepts a tuple specifying the minimum and maximum sizes of the n-grams.
```Python
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


# Term Frequency --- Inverse Document Frequency (TF-IDF)

## The TF-IDF Value
* The TF-IDF Value measures the importance of a word
	* TF is the frequency of occurrence of a word in a text
	* IDF is a measure of how common it is in the corpus

## Importance of TF-IDF Values
* Bag-of-words can fail to prioritize an important word because it takes word frequency into account
* Words that don't appear often might not be considered important, even if they carry alot of weight

## TF-IDF Formulas
* General Formula: 
	* $TF$ - Term Frequency
	* $IDF$ - Inverse Document Frequency $$TFIDF = TF * IDF$$
* Calculating TF: 
	* $t$  -- the number of word occurrences
	* $n$ -- the total number of words in the text $$TF = t/n$$
* Calculating IDF:
	* The role of IDF in the formula is to decrease the importance of the most commonly used words in any text within the given corpus.
		* $D$ -- the total number of texts in a corpus
		* $d$ -- the number of texts where the specific word occurs $$IDF = log_10 D/d$$


### Example: Using TF-IDF
* Consider a corpus that consists of twenty poems. The first poem has 40 words. Interested in the word 'river', which appears 5x in the poem. Find the TF-IDF for 'river' in the first poem of the corpus
	* Calculate TF $$TF = t / n = 5 / 40 = 0.125$$
	* Calculate IDF: Two out of twenty poems in the corpus have "river." So, IDF is equal to $$IDF = log_10 20 / 2 = 1$$
	* Calculate TF-IDF: $$TFIDF=TF*IDF = 0.125 * 1 = 0.125$$


## TF-IDF in Sklearn
* The `sklearn.feature_extraction.text` module has the `TfidfVectorizer()` class, which can be used to calculate the TF-IDF 
	* The n-grams can be calculated using the `TfidfVectorizer()` class by passing the `ngram_range=` argument into the class
* Steps:
	- Load the necessary libraries.
	- Import required modules from the `nltk` library.
	- Specify the stop words to be used.
	- Instantiate the `TfidfVectorizer()` class.
	- Compute the TF-IDF values for the text corpus using `fit_transform()`.
	    - When to `fit()` vs `fit_transform()`
		    - Use `fit()` when you are training the vectorizer on the training data only:
			    - This ensures that the model does not get biased by information from the test data.
			    - Follow it up with `transform()` on both your training and test data.
			- Use `fit_transform()` when you want to both fit and transform the training data in one step.
				- This is typically done only on the training dataset to prepare it for training the model.
```Python
# Using fit() then transform()

# Fit on training data
count_tf_idf.fit(train_corpus)

# Transform both training and test data
X_train = count_tf_idf.transform(train_corpus)
X_test = count_tf_idf.transform(test_corpus)
```

```Python
# Using fit_transform()
tf_idf = count_tf_idf.fit_transform(train_corpus)
```

```Python
# Import the class & nltk packages
from sklearn.feature_extraction.text import TfidfVectorizer
from nltk.corpus import stopwords
import nltk

# Define the stop words
stop_words = set(stopwords.words('english'))

# Create a counter
count_tf_idf = TfidfVectorizer(stop_words=stop_words)

# Calculate the TF-IDF for the text corpus
tf_idf = count_tf_idf.fit_transform(corpus)
```

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

submission.to_csv('predictions.csv', index=False)
```


# Sentiment Analysis
## What is Sentiment Analysis?
* Sentiment analysis identifies emotionally-charged texts.
	* Useful in business when evaluating consumer reactions to a new product

## How does Sentiment Analysis Work?
* Sentiment analysis works by labeling text as positive or negative. 
	* Positive text is given a "1"
	* Negative text is assigned a "0"
```Python
import pandas as pd
from nltk.corpus import stopwords as nltk_stopwords
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.metrics import accuracy_score
from sklearn.linear_model import LogisticRegression

# Load training data
train_data = pd.read_csv('/datasets/imdb_reviews_small_lemm_train.tsv', sep='\t')

# Load testing data
test_data = pd.read_csv('/datasets/imdb_reviews_small_lemm_test.tsv', sep='\t')

# Prepare training data
train_corpus = train_data['review_lemm']

# Get stop words in English
stop_words = set(nltk_stopwords.words('english'))

# Initialize TF-IDF vectorizer and fit-transform on training corpus
count_tf_idf = TfidfVectorizer(stop_words=stop_words)
tf_idf = count_tf_idf.fit_transform(train_corpus)

X_train = tf_idf
y_train = train_data['pos']

# Prepare test data
test_corpus = test_data['review_lemm']
X_test = count_tf_idf.transform(test_corpus)

# Create the model
model = LogisticRegression()

# Fit the model 
model.fit(X_train, y_train)

# Predict using test set
pred_test = model.predict(X_test)

# Download as CSV
submission.to_csv('predictions')
```


# Word Embeddings
## What are Word Embeddings?
* Machines cannot work directly with words, images, and audio because they are designed to work with numbers
* **Word embeddings** -- are a set of techniques that language models use to transform text into vectors.
	* Different areas in that vector space have different meanings from the language perspective.
	* A vector made from a word using word embedding will carry some contextual information about the word and its semantic properties.

## What is Semantic Meaning?
* Semantic properties are the components of a word that contribute to its meaning.
	* Separates words like: "male", "occupation", "etc" from other words


## Why are Word Embeddings Useful?
* Word embeddings enable the conversion of words into vectors that contain their semantic meanings.
	- This ensures that words with similar contexts have similar vectors.
	- The distance (cosine, Euclidean, etc.) between vectors reflects the relation between the meanings of words.

## Example: Understanding Word Embeddings
* 

![[word-embeddings.png]]



# Word2Vec
## What is Word2Vec?
* **Word2Vec** -- a method used to convert words into vectors so that semantically close words will get vectors close to each other. 

## Libraries with Word2Vec Services
* [spaCy](https://spacy.io/models/en)
* [Gensim](https://github.com/piskvorky/gensim-data)

## How do Word2Vec Libraries Work?
- word2vec libraries, typically include pre-trained word2vec models, each trained on a specific corpus of texts.
    - To get relevant vectors for specific texts, a word2vec model trained to a semantically relevant corpus of texts should be used.
- word2vec models can also address specific NLP tasks, such as:
    - Predicting whether certain words are neighbors
    - Train a model to distinguish pairs of true neighbors from random pairs of neighbors


## Predicting if Words are Neighbors
### Predicting Neighbors
* Words are considered neighbors if they appear within the same "window" (maximum distance between words).
	* Each word in a pair serves as a feature, this means:
		* Each pair consists of two features.
		* The "target" is to determine whether the words in the pair are neighbors.

### Example: Predicting True and Random Neighbors
* True Neighbors
	* Original Text: 
		* Red beak of the puffin flashed in the blue sky
	* Text after Lemmatization: 
		* red beak puffin flash in blue sky
	* Predicting the word "puffin"
		* Closest neighbors are: "red", "beak", "flash", "in"
		* Creates four pairs of neighbors
			* puffin red
			* puffin beak
			* puffin flash
			* puffin in
	* Predicting the word "flash"
		* Creates four pairs of neighbors
			* flash beak
			* flash puffin
			* flash in
			* flash blue
	* "Roll the Window": This process can be repeated continuously across the entire text and get a full list of neighboring words.
	
* Random Neighbors --> Allows the model to tell positive examples from negative ones
	* Take random words from the corpus and pair them up


# Embeddings for Classification

## Classifying Text Corpuses
* To classify a text corpus, the model will consist of two blocks:
	1. Models for converting words into vectors: words are converted into numerical vectors.
	2. Classification models: vectors are used as features.
		![[embeddings-for-classification.png]]
## Steps for Classifying Text Corpuses
1. Before moving on to the vectorization of words, pre-processing needs to be performed:
	* Each text is tokenized (broken down into words)
	* Words are lemmatized (reduced to their root form).
		* More complex models, such as BERT, don't require this step because they understand word forms
		* The text is cleaned of any stop words or unnecessary characters
		* For some algorithms (e.g. BERT), special tokens are added to mark the beginning and end of sentences.
2. Each text acquires its own list of tokens after preprocessing.
3. The tokens are passed to the model, and the model vectorizes the tokens using a pre-compiled token vocabulary. The output are vectors of predetermined length formed for each text.
4. The features (vectors) are passed to the model. The model then predicts the tonality of the text: "0" — negative, or "1" — positive.


# BERT Model
## What is the BERT Model?
* The BERT (Bidirectional Encoder Representations from Transformers) Model is a neural network model created for language representation
	* The BERT algorithm is capable of "understanding" the context of a whole text, not just short phrases.
* The BERT model is frequently used in machine learning to convert texts into vectors.

## Other Language Representation Models
* BERT models inspired other language representation models:
	* FastText
	* GloVe (Global Vectors for Word Representation)
	* ELMO (Embeddings from Language Models)
	* GPT (Generative Pre-Training Transformer)
* GPT-3 and BERT are the most accurate 

## How is BERT Used?
* Existing BERT models that are pre-trained (by Google or, possibly, other contributors) on large text corpora are typically used. 
* Pre-trained BERT models work for 104 languages 

## How does BERT Work?
* BERT takes into account both immediate neighbors and more distant words. 
	* This allows BERT to produce accurate vectors with respect to the natural meaning of words.
* Example(s):
	* "The red beak of the puffin (MASK) in the blue (MASK)"
		* **MASK** represents unknown or masked words.
	* The model has to guess what these masked words are
	* The model learns to figure out whether the words in the sentence are related. 
		* The words "flashed" and "sky" are masked. 
		* If the words "crawled" instead of "flashed" is masked, the model wouldn't find a connection.

## Pre-Processing with BERT
* BERT has its own **tokenizer** based on the corpus it was trained on. 
	* Other tokenizers won't work with BERT, and lemmatization is not required.

### Steps to Pre-Processing with BERT
Steps: 
1. Import the NumPy, PyTorch, and transformers libraries 
2. Initialize the tokenizer as an instance of `BertTokenizer()` with the name of the pre-trained model using the `from_pretained()` method.
	* Loads the dictionary used to train the BERT model
3. Convert the text into IDs of tokens using the `encode()` method; the BERT tokenizer will return IDs of tokens rather than tokens.
	* Token IDs are numerical indices for tokens in the internal dictionary used by BERT
	* The `add_special_tokens=` parameter adds the beginning token (101) and end token (102)
4. Create the vectors and pad if needed
	* The BERT model accepts vectors of a fixed length (512 tokens, but 2 are reserved, one for the beginning and one for the end)
		* If shorter than 510, the end of the vector should be padded with zeros
		* If larger than 510, some identifiers returned from are usually skipped
5. Discard tokens where the value is 0 and mask important tokens, using zero and non-zero numbers
	* Tells the model that these values (0) don't carry important info
```Python

# 1) Import libraries
import numpy as np
import torch
import transformers

# 2) Initialize the tokenizer as an instance of BertTokenizer() with pre-trained model
tokenizer = transformers.BertTokenizer.from_pretrained('bert-base-uncased')

# 3) Convert the text into IDs of tokens
example = 'It is very handy to use transformers' 
ids = tokenizer.encode(example, add_special_tokens=True) 
print(ids) # [101, 2009, 2003, 2200, 18801, 2000, 2224, 19081, 102]

# 4) Create the vector, pad if needed
n = 512

# Pad the vector with zeros if shorter than 512
padded = np.array(ids[:n] + [0]*(n - len(ids)))
print(padded) # [101 2009 2003 2200 18801 2000 2224 19081 102 0 0 0 0 ... 0 ]

# 5) Discard tokens where the value is 0 and mask important tokens
attention_mask = np.where(padded != 0, 1, 0)
print(attention_mask.shape) # (512, )
```

* Manually set the maximum length of the input
```Python
# 1) Import libraries
import numpy as np
import torch
import transformers

# 2) Initialize the tokenizer as an instance of BertTokenizer() with pre-trained model
tokenizer = transformers.BertTokenizer.from_pretrained('bert-base-uncased')

# 3) Convert the text into IDs of tokens

## Returns the full token list
example = 'It is very handy to use transformers'
ids = tokenizer.encode(example, add_special_tokens=True)
print(ids) # [101, 2009, 2003, 2200, 18801, 2000, 2224, 19081, 102]

## Returns a truncated token list
example = 'It is very handy to use transformers'
ids = tokenizer.encode(
   example, add_special_tokens=True, max_length=5, truncation=True
)
print(ids) # [101, 2009, 2003, 2200, 102]
```

```Python
# Full Example

import logging
import numpy as np
import pandas as pd
import torch
import transformers

# Load the dataset
data = pd.read_csv('/datasets/imdb_reviews_small.tsv', sep='\t')
# Initialize the tokenizer
tokenizer = transformers.BertTokenizer.from_pretrained('bert-base-uncased')

# Function to tokenize, pad and create attention masks
def tokenize_with_bert(texts):
    ids_list = []
    attention_mask_list = []
    min_tokenized_text_length = float('inf')
    max_tokenized_text_length = 0
    
    for text in texts:
	    # Tokenize the text
        ids = tokenizer.encode(
	        text.lower(), 
	        add_special_tokens=True, 
	        max_length=512, 
	        truncation=True
        )
        
        # Identify min and max lengths
        min_tokenized_text_length = min(min_tokenized_text_length, len(ids))
        max_tokenized_text_length = max(max_tokenized_text_length, len(ids))
        
        # Pad the tokenized text to 512 tokens
        padded = np.array(ids + [0] * (512 - len(ids)))
        
        # Create attention mask
        attention_mask = np.where(padded != 0, 1, 0)
        
        ids_list.append(padded)
        attention_mask_list.append(attention_mask)
    
    print(f'The minimum length of vectors: {min_tokenized_text_length}')
    print(f'The maximum length of vectors: {max_tokenized_text_length}')
        
    return ids_list, attention_mask_list

# Call the function with the dataset's reviews
ids_list, attention_mask_list = tokenize_with_bert(data['review'])
```

## BERT Embeddings

### What is Tensor?
* Tensor is a multidimensional vector that stores numbers in the "long format," allocating 64-bits to each number.

### Tensors
* Steps:
	1. Import the tqdm library from tqdm.auto
	2. Initialize the `BertConfig` configuration and pass a JSON file with the settings
	3. Initialize the `BertModel` class and pass it a pre-trained model and configuration
	4. Declare a batch size 
		* Make it small so that the RAM isn't overwhelmed
	5. Create a loop for the batches. Use the `tqdm()` function to indicate the progress
	6. Transform the data into a tensor format using the PyTorch library
	7. Pass the data and the mask to the model to obtain embeddings for the batch
	8. Use the **`no_grad()`** (no gradient) function to indicate that gradients are not needed. It will make calculations faster.
		* In the torch library (gradients are required for the training mode when creating your own BERT model). 
	9. Extract the required elements from the tensor and add the list of all the embeddings
	10. Concatenate all of the embeddings in a matrix of features using `np.concatenate()`
```Python
# 1. Import the tdqm library
from tqdm.auto import tqdm

# 2. Initialize the BERT cofiguration
config = BertConfig.from_pretrained('bert-base-uncased')

# 3. Initialize the BERT model
model = BertModel.from_pretrained('bert-base-uncased')

# 4. Declare a small batch size
batch_size = 100
embeddings = [] 

# 5. Create a loop for batches
for i in tqdm(range(len(ids_list) // batch_size)):
	# 6. Transform the data into a tensor format
	###  Putting together vectors of ids (of tokens) to a tensor
	ids_batch = torch.LongTensor(
		ids_list[batch_size*i:batch_size*(i+1)]
	)
	
	# Putting together vectors of attention masks to a tensor
	attention_mask_batch = torch.LongTensor(
		attention_mask_list[batch_size*i:batch_size*(i+1)]
	)
	
	# 7 & 8
	with torch.no_grad():
        batch_embeddings = model(
            ids_batch, attention_mask=attention_mask_batch
        )
        
    embeddings.append(batch_embeddings[0][:, 0, :].numpy())

# 10. Concatenate all the embeddings
features = np.concatenate(embeddings)
```

```Python
# Full Example

# --------- Import --------- #
import numpy as np
import pandas as pd

import torch
import transformers

from tqdm.auto import tqdm

from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import cross_val_score
from sklearn.model_selection import train_test_split

# --------- Global Variables --------- #
max_sample_size = 200

# --------- Import and Load Data --------- #
df_reviews = pd.read_csv(
	'/datasets/imdb_reviews_200.tsv', sep='\t'
)

# --------- Pre-processing for BERT --------- #
tokenizer = transformers.BertTokenizer.from_pretrained(
	'bert-base-uncased'
)

ids_list = []
attention_mask_list = []

max_length = 512

for input_text in df_reviews.iloc[:max_sample_size]['review']:
    ids = tokenizer.encode(
	    input_text.lower(), 
	    add_special_tokens=True, 
	    truncation=True, 
	    max_length=max_length
	)
    padded = np.array(ids + [0]*(max_length - len(ids)))
    attention_mask = np.where(padded != 0, 1, 0)
    ids_list.append(padded)
    attention_mask_list.append(attention_mask)

# --------- Global Embeddings --------- #
config = transformers.BertConfig.from_pretrained(
	'bert-base-uncased'
)
model = transformers.BertModel.from_pretrained('bert-base-uncased')

batch_size = 5   
embeddings = []

device = torch.device(
	'cuda' if torch.cuda.is_available() else 'cpu'
)

print(f'Using the {device} device.')

model.to(device)

for i in tqdm(range(len(ids_list) // batch_size)):
    ids_batch = torch.LongTensor(
	    ids_list[batch_size*i:batch_size*(i+1)]
	).to(device)
    
    attention_mask_batch = torch.LongTensor(
	    attention_mask_list[batch_size*i:batch_size*(i+1)]
    ).to(device)
    
    with torch.no_grad():
        model.eval()
        batch_embeddings = model(
	        ids_batch, attention_mask=attention_mask_batch
	    )
	    
    embeddings.append(
	    batch_embeddings[0][:,0,:].detach().cpu().numpy()
	)

# --------- Model --------- #
features = np.concatenate(embeddings)
target = df_reviews.iloc[:max_sample_size]['pos']

print(features.shape)
print(target.shape)

X_train, X_test, y_train, y_test = train_test_split(features, target, test_size=0.5, random_state=42)

model = LogisticRegression(random_state=12345)
model.fit(X_train, y_train)
y_pred = model.predict(X_test)

scores = cross_val_score(model, features, target, cv=5)
print(scores)
```