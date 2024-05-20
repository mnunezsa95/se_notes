See: [[CLI - What is the CLI?]], [[CLI - Command Line Basics?]]
Resource: 
* [Regex101: Check a pattern](https://regex101.com/)

---

## What are wildcards?
* Wildcards are special symbols that are used to describe patterns in a string that we might be interested in

## Main wildcards
* Here are some of the most common wildcards used in Linux systems.
	- `*` - asterisk
	- `?` - question mark
	- `[ ]` - square brackets
	- `{ }` - curly brackets
* Wildcards are case sensitive

#### Asterisk (`*`)
* `*` -- used to represent any sequence of characters (letters, numbers, and everything else), including an empty sequence.
```bash
# Remove all files that start with 'a' and end with `e`
rm a*e.py

# See all files in a directory that start with file_
ls file_x*.text
```

#### Question Marks (`?`)
* `?` -- used to represent exactly one character, rather than any number of characters like `*`
```bash
# Remove all files with only one character in between 'a' and 'e'
rm a?e.py # Will remove files like axe.py, age.py
```

#### Brackets `[]`
* `[ ]` -- used if we want to match particular characters that are enclosed in the brackets. 
	* Specify a subset of characters that we are interested in seeing in place of the `[ ]` pattern.
```bash
# Removing an file that starts with 'a', ends with 'e', and has any letter in the range a-g
rm a[abcdefg]e.py

# A simplified version
rm a[a-g]e.py

# Removing an file that starts with 'a', ends with 'e', and has any letter in the range a-g and A-G
rm a[a-gA-G].py
```

#### Curly Braces `{}`
* `{ }` -- used for multiple matches
```bash
# Remove all files with the .txt and .pdf extensions
rm {*.txt, *.pdf}

# Listing only files that either start with 'file' and have a 0,1,2 after or files that start and end with 'e' and have one character inbetween that is either 'v', 'w', 'y', 'z'
ls {file[0-2].txt,e[v-z]e.txt}
```