See: [[CLI - What is the CLI?]]

---
## Writing Commands
* Every command has a particular structure: `command [options...][arguments...]`
* Every command has a `--help` option to view possible options

## Commands
* A **command** is a program that tells the system what it needs to do.
	* Commands are case-sensitive 
	* Commands are executed with the 'enter' key
* Options are additional requests made alongside the command
	* Most options have two representations: one with a single hyphen and one with a double hyphen
		* Example: `ls -r` is the same as `ls --reverse`
```bash
# Printing content of the current directory in reverse order (also adding all hidden content)
ls -r -a

# Can also be written like this:
ls -ra
```
* Arguments tell the command to do 'something' with the the argument
```bash
# The ls command will run with the sql_project directory
ls -r sql_project
```