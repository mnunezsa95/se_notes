See [[Py - Introduction to Python]], [[Py - Functions]]

---

#### Function Flags
* Flags are usually boolean values that act like an on/off switch for certain behaviors of a function, and the switch usually has a default setting.
	* Built-in functions like the `sorted()` function have flags
* Flags are a common use case for Default Arguments

```Python
animals = ['Koala', 'antelope', 'Gibbon', 'Alligator', 'manatee', 'Capybara']

def sort_alph(words, change_case=True): # change_case is a flag in this instance
  sorted_words = []
  for word in words:
    sorted_words.append(word.lower())
  sorted_words = sorted(sorted_words)
  # convert first letter of sorted words to lowercase only if flag is True
    if change_case == False: 
      for i in range(len(sorted_words)):
        for j in range(len(words)):
          if sorted_words[i] == words[j].lower():
            sorted_words[i] = words[j]
    return sorted_words

without_flag = sort_alph(animals)
with_flag = sort_alph(animals, change_case=False)

print(without_flag) # ['alligator', 'antelope', 'capybara', 'gibbon', 'koala', 'manatee']
print(with_flag) # ['Alligator', 'antelope', 'Capybara', 'Gibbon', 'Koala', 'manatee']
```