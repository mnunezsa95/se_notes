See: [[CLI - What is the CLI?]], [[CLI - Command Line Basics?]]

---

## History

#### `history` command
* The `history` commands prints the commands that were previously run
```bash
# Printing a history of the commands run
history

# Priting the last 3 commands run
history 3

# Saving the history to a txt file
history > history.txt

# Checking the history for a particular command
history | grep pwd

# Checking the last 10 commands for the commands with the word 'python'
history 10 | grep python
history | tail 10 | grep python
history 10 | find . -name "*python*"
```

