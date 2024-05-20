See [[Py - Introduction to Python]], [[HTML - Introduction to HTML]]
Resources
* [How to Decode HTML Entities in Python](https://stackoverflow.com/questions/2087370/decode-html-entities-in-python-string) 

--- 
#### How to Escape HTML Entities in Python
1) Import the HTML module
```Python
import html
```
2) Use the `escape()` method
```python
question_data = get_questions.json()["results"]
html.escape(question_data)
```

