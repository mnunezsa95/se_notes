See [[Py - Introduction to Python]]

#### Root Folder
* Root Folder --> the main folder of all files 
	* MacOS --> Macintosh HD 
	* Windows --> C:
#### Absolute Paths
* Absolute File Paths are ALWAYS relative to the root
 * Example: Accessing quiz.txt
 **![](https://lh7-us.googleusercontent.com/k7UVdwbmWP6msrGUzpjlDsJlip1_Wi8O0c6gzsTbYP1iyoVf34jXfXe-NulDP-dUca9f7xX02T57KczrsjgiyPT3fi8-AtxS8FlhccciZUL-Ummk_9NH_gluafbxxcrsQaKKoEijfHluco9QChpyROc)**
```bash
/Users/my_project/quiz.txt
```

#### Relative Paths
* Relative File Paths are ALWATS relative to the current working directory
	* Using relative paths
		* Single dots (`./`) to go into a child folder
		* Double dots (`../`) to go up to a parent folder
		
 * Example 1: If you are writing code inside the **main.py** file to open the **quiz.txt** what would be the **relative** file path?
![](https://lh7-us.googleusercontent.com/yGi0LkT_nTlgwrh6XzPqzgocl1Dw_F3S3zpDYBHYdxBHVzMwJLbE5bbLMIOK6XpXe7kgGB0uAcRn_FSNRRB0WtHMZQgIiqV6T3s4zXozbgXOjQXWDcUJoaUothdjsAx1jz00epWH_g8cQV2IUkeGjLU)
```bash
quiz.txt
```

* Example 2: If you are writing code inside **main.py**, what is the **relative** file path to open **quiz.txt**?
**![](https://lh7-us.googleusercontent.com/UklEwL7IseVhIPVt84nLEX63_l-0bd7cLA9zQUCOo1aoPaZqAyVzPjtTCYs9sbxU4TqBJXSZqaaxv756mqfHQsbZfMWqeIuZx-mDRunE12b1PQsYlz7O9v4cXaTsgcpGpDFshcz222xe_sUm4tnJf9s)**
```bash
../my_files/quiz_files/quiz.txt
```

#### Differences between windows and Mac
* File paths in MacOS use `/`
* File paths in Windows use `\`
* In Python, it doesn't matter, use `/`