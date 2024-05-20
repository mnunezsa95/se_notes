See: [[CLI - What is the CLI?]], [[CLI - Command Line Basics?]]

---
## Environmental Variables

#### What are Environmental Variables?
* An **environment variable** is a variable whose value is set outside the program, typically through functionality built into the operating system or microservice. 
* An **environment variable** is made up of a name/value pair, and any number may be created and available for reference at a point in time.
* **Environmental variables** are available system-wide and are inherited by all processes.
#### Working with Environmental Variables
* Every variable in CLI starts with the `$` sign and has its name written in the upper case:
```Bash
# An enviro variable
$HOME

# Printing the environmental variable value
echo $HOME

# Printing all environmental variables
env

# Printing the value of the home environmental variable
printenv HOME
```

#### Shell Variables
* A **shell variable** is a character string in a shell that stores some value and ONLY exist in the current instance of the terminal
	* It could be an integer, filename, string, or some shell command itself. 
* A **shell variable** is a pointer to the actual data stored in memory. 

#### Main Differences: Environmental & Shell Variables
* The main difference between shell variables and environmental variables is that shell variables cannot be accessed in other programs or processes
* Environmental variables can be accessed by other programs & processes

#### Creating Shell Variables
```bash
# 1. Create the variable
MY_V="my first variable"

#2. Check that the variable was creates successfully
echo $MY_V

#3. Check the existence of this variable
printenv MY_V # Will be empty since MY_V is shell not environmental
```

#### Creating a Temporary Environmental Variable
* Custom environmental variables are available only in the current Terminal session. These are temporary environmental variables
* To create an environmental variable, create a shell variable, then export it
```bash
# 1. Create the variable
MY_V="my first variable"

# 2. Exporting the variable
export MY_V
```

#### Creating a Permanent Environmental Variable
Steps:
1. Open the terminal
2. Run the following code
```bash
sudo -H gedit /etc/environment
```

3. Type in password, if requested (the one to sign into computer)
4. Edit the text file that just opened (here is where you write your env variables). For example, if we want to add this env variable, `MY_V="my first variable"`, then we should type it in this file.
5. Save the text file

#### Accessing Environmental in Python Files
* Import the `os` library
* Extract the value needed
```python
# Importing the os library
import os

# Extracting the HOME environmental variable
os.environ["HOME"]
```