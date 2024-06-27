See:
* [[Py - Introduction to Python]]
* [[Py - ML (ML for Texts)]]
* [[Py - Transformers (Basics)]]
Resources
* TripleTen Knowledge Base: [Data Science](https://tripleten.netlify.app/)
* Documentation: [PyTorch](https://pytorch.org/docs/stable/index.html)
* Documentation: [transformers](https://huggingface.co/docs/transformers/en/index)

---
# Classes 

##### `BertTokenizer`
* Constructs a BERT tokenizer based on WordPiece.
	* Parameters
		* `vocab_file` (str) -- File containing the vocabulary.
		* `do_lower_case=` (bool) -- (`True`); Whether or not to lowercase the input when tokenizing.
		* `do_basic_tokenize=` (bool) -- (`True`); Whether or not to do basic tokenization before WordPiece.
		* `never_split=` (Iterable) -- Collection of tokens which will never be split during tokenization. 
			* Only has an effect when `do_basic_tokenize=True`
		* `unk_token=` (str) -- (`"UNK]"`); The unknown token. A token that is not in the vocabulary cannot be converted to an ID and is set to be this token instead.
		* `sep_token=` (str) -- (`"SEP"`); The separator token, which is used when building a sequence from multiple sequences, e.g. two sequences for sequence classification or for a text and a question for question answering. It is also used as the last token of a sequence built with special tokens.
		* `pad_token=` (str) -- (`"PAD"`); The token used for padding, for example when batching sequences of different lengths.
		* `cls_token=` (str) -- (`"CLS"`); The classifier token which is used when doing sequence classification (classification of the whole sequence instead of per-token classification). It is the first token of the sequence when built with special tokens.
		* `mask_token=` (str) -- (`"MASK"`); The token used for masking values. This is the token used when training this model with masked language modeling. This is the token which the model will try to predict.
		* `tokenize_chinese_chars=` (bool) -- (`True`); Whether or not to tokenize Chinese characters.
	* Methods
		* `from_pretrained()` -- Instantiates a `BertTokenizer()` from a pre-trained tokenizer.
			* Parameters:
				* `pretrained_model_name_or_path` (str or os.PathLike) -- The name or path to the pre-trained tokenizer
		* `encode()`
			* `text` (str, list) — The first sequence to be encoded. This can be a string, a list of strings (tokenized string using the `tokenize` method) or a list of integers (tokenized string ids using the `convert_tokens_to_ids` method).
			* `add_special_tokens=` (bool) -- (`True`); Whether or not to add special tokens when encoding the sequences.
			* `truncation=` (bool, str) -- (`False`); Activates and controls truncation. Accepts the following values:
				* `True` or `'longest_first'`: Truncate to a maximum length specified with the argument `max_length` or to the maximum acceptable input length for the model if that argument is not provided. This will truncate token by token, removing a token from the longest sequence in the pair if a pair of sequences (or a batch of pairs) is provided.
				- `'only_first'`: Truncate to a maximum length specified with the argument `max_length` or to the maximum acceptable input length for the model if that argument is not provided. This will only truncate the first sequence of a pair if a pair of sequences (or a batch of pairs) is provided.
				- `'only_second'`: Truncate to a maximum length specified with the argument `max_length` or to the maximum acceptable input length for the model if that argument is not provided. This will only truncate the second sequence of a pair if a pair of sequences (or a batch of pairs) is provided.
				- `False` or `'do_not_truncate'` (default): No truncation (i.e., can output batch with sequence lengths greater than the model maximum admissible input size).
			- `max_length=` (int) -- Controls the maximum length to use by one of the truncation/padding parameters.



strip_accents (bool, optional) — Whether or not to strip all accents. If this option is not specified, then it will be determined by the value for lowercase (as in the original BERT).
```Python
import transformers

model = transformers.BertTokenizer.from_pretrained('bert-base-uncased')
```