See: 
* [[Py - Introduction to Python]], 
* [[CLI - What is the CLI?]]
Resources
* Documentation: [argparse Library](https://docs.python.org/3/library/argparse.html)

---
## Understanding Python in the Command Line

#### Understanding Python in Command Line
* The line begins with (base), which signifies that we are using the base Anaconda environment.
	* The base environment means that we are using the version of Python that was installed with Anaconda and all the packages available to us as well (whichever package versions were installed).
```bash
(base) marlonnunez@Marlons-MacBook-Pro ~
```


## Running Python Code from the Command Line
#### Running Python Scripts from the Command Line
* To run a Python script from the command line, just type the command python followed by the path to the script file
	* Libraries used in a script must be installed before running the script in the CLI
```bash
# Running the cpus.py file in the terminal
(base) marlonnunez@Marlons-MacBook-Pro ~ % python cpus.py
```

#### Running Python Scripts from the Command Line (with Args, Options, and Flags)
* Arguments **MUST** be passed in positionally by including them in the command line execution statement. The argument values passed are used in within the script.
	* The `argparse` library can be used to create arguments for the CLI
* Options are optional arguments that can be included to change how the program works
	* Options are represented by a short or long form
		* Long: `--option=value` or `--option value`
		* Short: `-o=value`, `-o value`
	* Options must have default values, specified by the `default=` parameter in the `add_argument`
* Flags are boolean options that can only have `True` or `False` as options
	* Flags must have the `action=` parameter added to the `add_argument`
* Help messages can be added to the script in the `help=` parameter of the `add_argument()`
	* These messages show up when you run `-h` or `--help` in the command line
* Example:
```python
# image_rotator.py
from PIL import Image
import argparse

parser = argparse.ArgumentParser() # start parser

# adding arguments; stores all arguments as attributes of the args object
parser.add_argument('input_file', help='input file path')
parser.add_argument('output_file', help='output file path')
parser.add_argument('--angle', '-a', type=int, default=90) # adding option
parser.add_argument('-i', '--info' action='store_true') # adding flag

args = parser.parse_args() # parse
im = Image.open(args.input_file) # load
if args.info: # display image size if the info flag is added
  print('input image dimensions:', im.size) 
rotated = im.rotate(args.angle) # rotate once (counterclockwise)
rotated.save(args.output_file) # save
```

```bash
# Running the image_rotator.py file in the terminal with args
python image_rotator.py myimage.png output.png 180

# Running the image_rotator.py file in the terminal with args & options
python image_rotator.py myimage.png --angle=180 output.png

# Running the image_rotator.py file in the terminal with args, options & flags
python3 image_rotator.py myimage.png output.png 180 -i

# Running the help messages for the image_rotator.py script
python3 image_rotator.py -h
```

* Example: Running Python in the Command Line
```python
import argparse

parser = argparse.ArgumentParser()
parser.add_argument("first_name", help="person first name")
parser.add_argument("last_name", help="person last name")
parser.add_argument("age", type=int, help="person age")
parser.add_argument("--school", "-s", help="person school", default="Tulane")

args = parser.parse_args()

print(f"{args.first_name} {args.last_name} is {args.age} years old. He attended    {args.school}")
```

```bash
python3 test.py Marlon Nunez 28 -s="Boston U"
```

#### Running Python Code Interactively from the Command Line
* Entering `REPL` environment (Read Evaluate Print Loop)
```bash
# Entering interactive REPL mode
python
```
* Exiting `REPL` environment
```bash
# Exiting interactive REPL mode
exit()
```

* Features of `REPL` mode:
	* Used to run python code
	* Any variables created during `REPL` mode, are available until current session ends