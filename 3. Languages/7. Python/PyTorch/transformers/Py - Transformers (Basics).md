See:
* [[Py - Introduction to Python]]
* [[Py - ML (ML for Texts)]]
* [[Py - Transformers (Methods)]]
Resources
* TripleTen Knowledge Base: [Data Science](https://tripleten.netlify.app/)
* Documentation: [PyTorch](https://pytorch.org/docs/stable/index.html)
* Documentation: [transformers](https://huggingface.co/docs/transformers/en/index)

---

# What is transformers?
* Transformers provides APIs and tools to easily download and train state-of-the-art pre-trained models. Using pre-trained models can reduce your compute costs, carbon footprint, and save you the time and resources required to train a model from scratch. These models support common tasks in different modalities, such as:
	* 📝 **Natural Language Processing**: text classification, named entity recognition, question answering, language modeling, summarization, translation, multiple choice, and text generation.  
	* 🖼️ **Computer Vision**: image classification, object detection, and segmentation.  
	* 🗣️ **Audio**: automatic speech recognition and audio classification.  
	* 🐙 **Multimodal**: table question answering, optical character recognition, information extraction from scanned documents, video classification, and visual question answering.
* Transformers support framework interoperability between PyTorch, TensorFlow, and JAX. This provides the flexibility to use a different framework at each stage of a model’s life; train a model in three lines of code in one framework, and load it for inference in another. Models can also be exported to a format like ONNX and TorchScript for deployment in production environments.

# Installing transformers
## Install using pip
* Installing PyTorch using the following bash command:
```bash
# Start by creating a virtual environment in your project directory:
python -m venv .env

# Activate the virtual environment. On Linux and MacOs:
source .env/bin/activate

# Install
pip install transformers
```

## Install using Conda
```bash
conda install conda-forge::transformers
```

# Importing transformers
```Python
import transformers
```