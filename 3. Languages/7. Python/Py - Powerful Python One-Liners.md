See [[Py - Introduction to Python]]
Resources
* [60 Powerful Python One-Liners for Everyday Coding Tasks](https://python.plainenglish.io/60-powerful-python-one-liners-for-everyday-coding-tasks-94cafe16ca85)

---

#### 1. Print the systems’s hostname:
```python
from socket import gethostname; print gethostname()
```
#### 2. Decode string written in Hex:
```python
python -c "print ''.join(chr(int(''.join(i), 16)) for i in zip(*[iter('474e552773204e6f7420556e6978')]*2))"
```
#### 3. Read Lines from a File:
```Python
lines = [line.strip() for line in open('example.txt')]
```
#### 4. Count Lines in a File:
```Python
line_count = sum(1 for line in open('example.txt'))
```
#### 5. Extract Digits from a String:
```python
digits = ''.join(filter(str.isdigit, my_string))
```
#### 6. List Comprehension with Conditional:
```python
filtered_list = [x for x in my_list if x > 0]
```
#### 7. Remove Duplicates from a List:
```python
unique_list = list(set(original_list))
```
#### 8. Calculate Average of a List:
```python
average = sum(my_list) / len(my_list) if len(my_list) > 0 else 0
```
#### 9. Generate Fibonacci Sequence:
```python
fibonacci = lambda n: n if n <= 1 else fibonacci(n-1) + fibonacci(n-2)
```
#### 10. Conditional Value Assignment:
```python
result = x if condition else y
```