See: [[CLI - What is the CLI?]], [[CLI - Command Line Basics?]]

---

## Piping

#### What is piping?
* Pipes in CLI transfer the output of one command to the input of another.
#### Example(s) of Piping:
* Example 1:
	* How it works: listed out the contents of a directory using ls and then used a pipe (|) to pass the output of ls to the next command (grep). From here, grep takes the ls output as its input and performs a search for the word data. 
```bash
ls | grep "data"
```
* Example 2:
	* How it works: Take the output of the ls command and only display the last line of it by using the `tail -1`  command:
```bash
ls | tail -1
```
* Example: 3
	* How it works: This command opens `super_text_file.txt`, selects all lines that have the word `python` in it, and then displays the first 3 lines.
```bash
cat super_text_file.txt | grep "python" | head -3
```