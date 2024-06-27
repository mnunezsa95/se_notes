See:
* [[Py - Introduction to Python]]
* [[Py - ML (ML for Texts)]]
* [[Py - NLTK (Basics)]]
Resources
* TripleTen Knowledge Base: [Data Science](https://tripleten.netlify.app/)
* Documentation: [Pandas](https://pandas.pydata.org/docs/)
* Documentation: [NumPy](https://numpy.org/doc/stable/index.html)
* Documentation: [SK-Learn](https://scikit-learn.org/stable/)
* Documentation: [SciPy](https://docs.scipy.org/doc/scipy/index.html)
* Documentation: [NLTK](https://www.nltk.org/)

---

# Classes

##### `nltk.stem.WordNetLemmatizer()`
* Lemmatizes a word using WordNet’s built-in morphy function. Returns the input word unchanged if it cannot be found in WordNet.
	* Parameters
		* `word` (str) -- The input word to lemmatize.
		* `pos` (str) -- The Part Of Speech tag. Valid options are:
			* `“n”` for nouns 
			* `“v”` for verbs
			* `“a”` for adjectives
			* `“r”` for adverbs
			* `“s”` for satellite adjectives
```Python
from nltk.stem import WordNetLemmatizer

wnl = WordNetLemmatizer()
print(wnl.lemmatize('dogs')) # dog
print(wnl.lemmatize('churches')) # church
print(wnl.lemmatize('aardwolves')) # aardwolf
print(wnl.lemmatize('abaci')) # abacus
print(wnl.lemmatize('hardrock')) # hardrock
```


# Methods

##### `nltk.download()`
* Downloads the specified package(s)
	* `package` -- The package to download
```Python
import nltk
from nltk.corpus import stopwords

nltk.download('stopwords')
```


##### `nltk.corpus.stopwords.words()`
* Retrieves the stop words for a particular language
	* Parameters
		* `language` -- The language for which stop words should be retrieved
```Python
import nltk
from nltk.corpus import stopwords

nltk.download('stopwords')
stop_words = set(stopwords.words('english'))
```

##### `nltk.tokenize.word_tokenize()`
* Returns a tokenized copy of _text_, using NLTK’s recommended word tokenizer
	* Parameters
		* `text` (str) -- text to split into words
		* `language` (str) -- the model name in the Punkt corpus
		* `preserve_line` (bool) -- A flag to decide whether to sentence tokenize the text or not.
```Python
text = "All models are wrong, but some are useful."
tokens = word_tokenize(text.lower())
```