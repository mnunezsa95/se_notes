See: [[CLI - What is the CLI?]], [[CLI - Command Line Basics?]]

---

## Search Commands

#### `find` command
* The `find` command searches for both files and directories based on a set of conditions
* The `find` command expects multiple arguments
	* Each argument is a path to a directory, and the search should happen
```bash
# Searching for a particular name in the current directory
find . -name file2find.txt

# Searching for a particular name in the current directory (name can have upper and lowercase words)
find . -iname file2find.txt

# Limitng the search to only directories
find . -type d -iname to_find

# Limitng the search to only files with any name
find . -name "*o_find"

# Limiting the search to files that were modified 2 days ago
find . -mtime 2

# Limitng the search to files that were changed 120 mins ago
find . -cmin -120

# Deleting items that match the criteria
 find . -name "*.txt" -delete 
```

```Bash
# Result of running: find . -name file2find.txt
./file2find.txt

# Result of running: find . -iname file2find.txt
./file2find.txt
./File2find.txt

# Result of running: find . -type d -iname to_find
./to_find

# Result of running: find . -name "*o_find"
./to_find
./To_find
```

#### `grep` command
* The `grep` command searches for patterns in the contents of a file
```bash
# Display the lines of a file that contain the target words "text"
grep "text" another_text_file.txt

# Displaying the lines of a file that are exact matches with 'text'
grep -w "text" another_text_file.txt

# Displaying the lines of a file that are exact matches with 'text' and are case insensitive
grep -iw "text" another_text_file.txt

# Displays all files located in the current directory that have either 'text' or "Text"
grep -iw "text" *

# Counts how many times the search word appears in the specified file
grep -c "text" another_text_file.txt # 2

# Find and lists the files that have the specified word in them
grep -l "text" another_text_file.txt text_file_1.txt text_file_2.txt
```

```bash
# Result of running: grep "text" another_text_file.txt
Heres some text.
What about the word "textile"?

# Result of running: grep -w "text" another_text_file.txt
Heres some text.

# Result of running: grep -iw "text" another_text_file.txt
Text files are great.
Here's some text.
```