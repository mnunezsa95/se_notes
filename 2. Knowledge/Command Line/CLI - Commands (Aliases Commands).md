See: [[CLI - What is the CLI?]], [[CLI - Command Line Basics?]]

---

## Aliases
* An alias is just a string that is typed in the command-line interface. 
* This string is a shortcut that references a command. 

#### `alias` command
* The `alias` command prints a list of the default aliases listed
* Syntax
	* `name` is the alias name that we want to set.
	* `value` is the command that we want to invoke. 
```bash
alias name='value'
```

```bash
# Seeing a list of aliases
alias

# Creating a new alias
alias cdp="cd /home/jovyan/work/my_amazing_project"

# Creating a new alias
alias smv="mv -i"
```

#### Permanent Aliases
* To make an alias permanent between sessions, we use the same logic as temporary aliases, but it is done in a configuration file called `.bashrc`.
* The `.bashrc` is usually already created and found in home directory:
```bash
# Can be found using this address
~./bashrc
```

```bash
# Opening the bashrc file
vi ~./bashrc

# Adding two aliases
alias cdp="cd /home/my_amazing_project"
alias smv="mv -i”

```