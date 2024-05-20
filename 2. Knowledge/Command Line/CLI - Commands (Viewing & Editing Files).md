See: [[CLI - What is the CLI?]], [[CLI - Command Line Basics?]]

---

## Viewing & Editing Files

#### cat `command`
* The `cat` command will print the contents of a txt file in the terminal
* The `cat` command can create a file or append the content from one file to another
```Bash
# Opening a text file in the terminal
cat my_file.txt

# Viewing the content of two different files
cat file2display.txt file2display_2.txt

# Creating a file using cat (will overwrite if file already exists)
cat > my_text_file.txt

# Adding content to an exisiting file (not overwriting)
cat >> my_text_file.txt

# Copying the content from one file to another
cat file2display.txt > another_text_file.txt
cat another_text_file.txt
```

#### `wc` command
* The `wc` command (word count) counts the number of lines, words, and bytes in a file
```bash
# Printing the line, word, and byte count
echo lets practice the wc command > wc_file.txt
wc wc_file.txt

# Priting the line, word, and byte count of a multiple files
wc wc_file.txt file2display.txt
```

```Bash 
# Resulting from running: wc wc_file.txt file2display.txt
1  5 29 wc_file.txt
1  3 19 file2display.txt
2  8 48 total
```

#### `head` command
* The `head` command prints the first lines (10 by default) of the file
```bash
head -n 4 names.txt
```

```bash
# Result of running head -n 4 names.txt

zach
brian
robert
john
```

#### `tail` command
* The `tail` command prints the last lines (10 by default) of the file
```bash
tail -n 4 names.txt
```

```bash
# Result of running tail -n 4 names.txt

anthony
alex
jeremy
zach
```

#### `vi` command
* Opens the default text editor for UNIX operating systems
* Operates in its own environment (not terminal, but VI environment)
* VI has 2 main modes:
	* Command Mode (*what it opens up in*) -- the mode where every character that we type in is treated as a part of a command.
	* Insert Mode -- the mode that we use to type the actual text that we want to insert into the file. 
		* To enter _Insert Mode,_ press `i` on the keyboard
		* To exit _Insert Mode,_ press `esc` on the keyboard
* Popular commands
	* `:wq` -- to save the text to the file and quit.
	* `ZZ` -- to save if there were any changes and quit. Works similarly to `:wq`.
	* `:q` -- to quit. This command will only work if a file has not been modified.
	* `:q!` -- to quit the file without saving any changes.
	* `dd` to delete a selected line;
	- `x` to delete a selected character;
	- `r` to replace a selected character.
```bash
# Creates a new file and opens it
vi my_new_text_file.txt

# Editting an existing file
vi my_new_text_file.txt
```