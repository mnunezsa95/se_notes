See [[Py - Introduction to Python]], [[Py - Pandas (Installing & Importing Pandas)]],
Documentation
* [Pandas Documentation](https://pandas.pydata.org/docs/)


---
#### Sample Space Probabilities 
* Simple probability calculations can be done using `==` & `len()`
	* `==` -> will find the rows that satisfy an event
	* `len()` will return the number of rows that satisfy an event
* Example
```python
import pandas as pd

ya_music_rock = pd.DataFrame(
  {
    'Artist': ['Queen', 'Queen', 'Queen', 'Pink Floyd', 'Nirvana', 'AC/DC',                     'AC/DC', 'Scorpions', 'Scorpions', 'Scorpions' ],
    'Song': ['The Show Must Go On','Another One Bites The Dust', 
             'We Will Rock You', 'Wish You Were Here', 'Smells Like Teen Spirit',
             'Highway To Hell', 'Back in Black', 'Wind Of Change', 
             'Still Loving You', 'Send Me An Angel'],
  }
)

# What's the probability that the first song will be "Smells Like Teen Spirit"?
len(ya_music_rock[ya_music_rock['Song'] == 'Smells Like Teen Spirit']) / len(ya_music_rock) # 0.1 
```
