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
Resources:
* TripleTen Knowledge Base: [Data Science](https://tripleten.netlify.app/)
* Documentation: [Pandas](https://pandas.pydata.org/docs/)
* Documentation: [NumPy](https://numpy.org/doc/stable/index.html)
* Documentation: [SK-Learn](https://scikit-learn.org/stable/)
* Documentation: [SciPy](https://docs.scipy.org/doc/scipy/index.html)
* Documentation: [NLTK](https://www.nltk.org/)
* Documentation: [spaCy](https://spacy.io/)

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

```Python
# Using a Counter() results in the same output
import spacy
from collections import Counter

nlp = spacy.load('en_core_web_sm', disable=['parser', 'ner'])

text = """For want of a nail the shoe was lost. For want of a shoe the horse was lost. For want of a horse the rider was lost."""

doc = nlp(text)

tokens = [token.lemma_ for token in doc if not token.is_punct]
bow = Counter(tokens)
vector = [bow[token] for token in sorted(bow)]

print(vector) # [3, 3, 3, 2, 3, 1, 3, 1, 2, 3, 3]
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

