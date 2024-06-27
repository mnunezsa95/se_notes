See:
* [[Py - Introduction to Python]]
* [[Py - ML (ML for Texts)]]
* [[Py - spaCy (Methods)]]
Resources
* TripleTen Knowledge Base: [Data Science](https://tripleten.netlify.app/)
* Documentation: [Pandas](https://pandas.pydata.org/docs/)
* Documentation: [NumPy](https://numpy.org/doc/stable/index.html)
* Documentation: [SK-Learn](https://scikit-learn.org/stable/)
* Documentation: [SciPy](https://docs.scipy.org/doc/scipy/index.html)
* Documentation: [spaCy](https://spacy.io/)


----
# What is spaCy?
* spaCy is an open-source software library for advanced Natural Language Processing (NLP) in Python. Designed specifically for production use, it is known for its performance, ease of use, and robust ecosystem of tools and resources. Here are some key features and aspects of spaCy:
	1. **Tokenization**: Efficiently breaks down text into tokens (words, punctuation, etc.).
	2. **Linguistic Features**: Provides detailed linguistic annotations, including part-of-speech tagging, dependency parsing, named entity recognition (NER), and more.
	3. **Pre-trained Models**: Includes pre-trained statistical models for multiple languages, enabling quick deployment of NLP tasks without the need for extensive training.
	4. **Training and Custom Models**: Supports training custom models for specific tasks or domains.
	5. **Integration**: Works well with other popular NLP libraries and frameworks, such as TensorFlow and PyTorch, and can be integrated into larger machine learning pipelines.
	6. **Extensibility**: Offers the ability to add custom components and extend existing ones, making it highly customizable.
	7. **Efficient and Production-Ready**: Focuses on speed and efficiency, making it suitable for real-time applications and large-scale processing.

## Common Uses for spaCy
* Common use cases for spaCy include 
	* Text classification
	* Information extraction
	* Question answering
	* Machine translation
* Its robust documentation and active community also make it a popular choice for both beginners and advanced users in the NLP field.

# Installing spaCy 
* Can be installed using pip or conda
## Using pip
* Using `pip`, spaCy releases are available as source packages and binary wheels. 
* Before installing spaCy and its dependencies, make sure that `pip`, `setuptools` and `wheel` are up to date.
```Bash
# Install spaCy
pip install -U pip setuptools wheel
pip install -U spacy
```
* When using pip it is generally recommended to install packages in a virtual environment to avoid modifying system state:
```bash
python -m venv .env
source .env/bin/activate
pip install -U pip setuptools wheel
pip install -U spacy
```

## Using conda
```bash
conda install -c conda-forge spacy
```

# Importing spaCy
* Use the `import` keyword to import NLTK
```Python
import spacy
```