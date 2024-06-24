See:
* [[Py - Introduction to Python]]
* [[Py - ML (ML for Texts)]]
* [[Py - spaCy (Basics)]]
Resources
* TripleTen Knowledge Base: [Data Science](https://tripleten.netlify.app/)
* Documentation: [Pandas](https://pandas.pydata.org/docs/)
* Documentation: [NumPy](https://numpy.org/doc/stable/index.html)
* Documentation: [SK-Learn](https://scikit-learn.org/stable/)
* Documentation: [SciPy](https://docs.scipy.org/doc/scipy/index.html)
* Documentation: [NLTK](https://www.nltk.org/)
* Documentation: [spaCy](https://spacy.io/)

---

# Classes




# Methods

##### `spacy.load()`
* Loads a pipeline using the name of an installed [package](https://spacy.io/usage/saving-loading#models), a string path or a `Path`-like object.
	* Parameters
		* `name` (str) -- Pipeline to load, i.e. package name or path.
		* `vocab=` (str) -- Optional shared vocab to pass in on initialization.
			* If `True` (default), a new `Vocab` object will be created.
		* `disable=` (str) -- Name(s) of pipeline component(s) to [disable](https://spacy.io/usage/processing-pipelines#disabling)
		* `enable=` (str) -- Name(s) of pipeline component(s) to [enable](https://spacy.io/usage/processing-pipelines#disabling). 
			* All other pipes will be disabled.
		* `exclude=` (str) -- Name(s) of pipeline component(s) to [exclude](https://spacy.io/usage/processing-pipelines#disabling). Excluded components won’t be loaded.
		* `config=` (str) -- Optional config overrides, either as nested dict or dict keyed by section value in dot notation, e.g. `"components.name.value"`.
```Python
import spacy
nlp = spacy.load('en_core_web_sm', disable=['parser', 'ner'])
doc = nlp(text.lower())
lemmas = [token.lemma_ for token in doc]
print(" ".join(lemmas))
```
# Attribute
##### `token.lemma_`
* Contains predictions
```Python
import spacy
nlp = spacy.load('en_core_web_sm', disable=['parser', 'ner'])
doc = nlp(text.lower())
lemmas = [token.lemma_ for token in doc]
print(" ".join(lemmas))
```
