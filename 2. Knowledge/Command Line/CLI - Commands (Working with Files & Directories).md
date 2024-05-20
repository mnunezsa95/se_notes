See: [[CLI - What is the CLI?]], [[CLI - Command Line Basics?]]

---

## Working with Files & Directories

#### `mkdir` command
* `mkdir` command is used to create new directories 
```Bash
# Creating a new directory
mkdir my_new_directory

# Creating 3 new directories
mkdir my_new_directory1 my_new_directory2 my_new_directory3

# Creating a subdirectory within a parent directory
mkdir my_parent_dir/my_sub_dir

# Creates a subdirectory and parent directory
mkdir -p my_parent_dir/my_sub_dir

# Shows what is being done by two commands
mkdir -p -v my_parent_dir/my_sub_dir
```

```bash
# Resulting of running: mkdir -p -v my_parent_dir/my_sub_dir

mkdir: created directory 'my_parent_dir'
mkdir: created directory 'my_parent_dir/my_sub_dir'
```

#### `rm` command
* `rm` command removes files and directories
```bash
# Removes a directory
rm my_new_directory

# Removes an empty directory
rm -d my_new_directory

# Remove the empty directory & show what happened
rm -d -v my_new_directory

# Removing multiplying directories
rm file1 file2 file3

# Prompting an interactive message before removing directory
rm -d -i my_new_directory
```

```bash
# Result of running: rm -d -v my_new_directory
removed directory 'my_new_directory/'

# Result og running: rm -d -i my_new_directory
rm: remove directory 'my_new_directory/'?
```

#### `echo` command
* `echo` is a [built-in command](https://www.computerhope.com/jargon/b/builtin.htm) used to print out arguments in the _Terminal_ as standard output
```bash
# Printing 'I want to know CLI' in the terminal
echo I want to know CLI

# Printing 'I want to know CLI' in the terminal using escape characters
echo -e 'I want to know CLI. \nEvery programmer knows it!'

# Redirecting the output to a text file (if it does not exist, file will be created)
echo -e 'I want to know CLI. \nEvery programmer knows it!' > my_file.txt

# Redirecting the output to a text file (adding a new line, not overwriting)
echo -e 'I want to know CLI. \nEvery programmer knows it!' >> my_file.txt
```

```bash
# Result of running: echo I want to know CLI
I want to know CLI

# Result of running: echo -e 'I want to know CLI. \nEvery programmer knows it!'
I want to know CLI. 
Every programmer knows it!
```


#### `touch` command
* The `touch` command creates a file in the working directory
```bash
# Creating a file called 'my_new_file'
touch my_new_file
```

#### `mv` command
* The `mv` command moves a file or directory from one location to another
```bash
# Moving a file to a new directory
mv my_file.txt sub_directory

# Moving a file to a directory located outside of the current one
mv my_file.txt ~/home_sub_directory

# Moving multiple files to a director located outside the current one
mv my_file1.txt my_file2.txt ~/home_sub_directory

# Moving a directory to a new directory
mv sub_directory ~/home_sub_directory
```

#### `cp` command
* The `cp` command copies a file or directory
```bash
# Copying a file
cp original_file.txt copy_from_original.txt

# Copying a directory & its content to a different directory in a different location
cp -r my_files ~/home_sub_directory


```