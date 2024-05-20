See:
* [[Py - Introduction to Python]]
* [[HTML - Introduction to HTML]]
* [[Py - Installing Packages, Modules, and Libraries]]
Resources:
* Documentation: [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)

---
# Web Scrapping

## Intro to BeautifulSoup
* BeautifulSoup methods turn an HTML file into a tree structure, allowing for the necessary content to be found using tags and attributes
![[HTML-tree.jpg]]

### Installing BeautifulSoup
* BeautifulSoup can be installed using `pip`
```bash
pip install beautifulsoup4
```
### Importing BeautifulSoup
* `BeautifulSoup` is in the `bs4` module
```Python
from bs4 import BeautifulSoup
```


---
# Working with BeautifulSoup 
## Creating a BeautifulSoup Object
* The `BeautfulSoup` class is used to create an object
	* Arguments
		* `data` -- the data that will form the tree structure
		* `parser` -- defines the way the webpage is turned into a tree
			* `lxml` -- high-speed performance
			* `html.parser`
			* `xml`
			* `html5lib`
```Python
from bs4 import BeautifulSoup
soup = BeautifulSoup(req.text, 'lxml')
```

#### `prettify()`
* Nicely formats and indents the HTML document in Python
	* Arguments
		* None
```Python
# Example -- Using the prettify() Method

from bs4 import BeautifulSoup

with open("day_45/website.html") as html_file:
	contents = html_file.read()

soup = BeautifulSoup(contents, "html.parser")

# Printing a nicely formatted version of the HTML document in the console
print(soup.prettify()) 
```


---
## Accessing Content using BeautifulSoup
* There are two ways to access content 
	* Using properties of the BeautifulSoup object 
	* Using BeautifulSoup Methods
		* `find()`
		* `find_all()`
		* `select()`
		* `select_one()`
		* `get()`
```Python
# Example -- Accessing items using properties

# Importing BeautifulSoup
from bs4 import BeautifulSoup

# Opening an HTML file using Python
with open("day_45/website.html") as html_file:
    contents = html_file.read()

# Creating a BeautifulSoup object
soup = BeautifulSoup(contents, "html.parser")

print(soup.title) # Accessing the first title (<title>) tag
print(soup.title.name) # Acessing the string inside the first <title> tag
print(soup.a) # Accessing the first anchor (<a>) tag
```

#### `find()`
* Finds the first element whose name was passed as an argument and returns it together with the element's tag and content
	* Arguments
		* `element` -- the element to search for
		* `attrs=` -- looks for classes and identifiers; accepts a dictionary with attribute names and values

* The `text` attribute can be used to display the content without the tags
```Python
# Example -- Using the find() method

# Accessing the FIRST item with an <h2> tag
heading_2 = soup.find("h2") 
print(heading_2) # <h2> The Biggest Shipwrecks of the 20th Century </h2>
print(heading_2.text) # The Biggest Shipwrecks of the 20th Century
```

```Python
# Example -- Using the find() method

# Accessing the FIRST item with an <h1> tag and an ID of 'name'
heading = soup.find(name="h1", id="name")
print(heading)
```

```Python
# Example -- Using the find() method

# Accessing the FIRST item with an <h3> tag and a class of 'heading'
section_heading = soup.find(name="h3", class_="heading")

print(section_heading)
print(section_heading.name)
print(section_heading.get("class"))
```

#### `find_all()`
* Finds _all_ the instances of a given element in a tree and returns a list
	* Arguments
		* `element` -- the element to search for
		* `attrs=` -- looks for classes and identifiers; accepts a dictionary with attribute names and values
```Python
# Example -- Using the find_all() method

# Accessing all items with a <p> tag
paragraph = soup.find_all('p')
print(paragraph) # ["abcdefgh", "ijklmno", "qrstuv"]

for paragraph in soup.find_all('p'):
    print(paragraph.text) # abcdefgh ijklmno qrstuv
```

```Python
# Example -- Using the find_all() method

# Accessing ALL items with an <a> tag
all_anchor_tags = soup.find_all(name="a")
print(all_anchor_tags)

# Iterating through the list and accessing the text of the tag, and the link of the tag
for tag in all_anchor_tags:
    print(tag.getText())
    print(tag.get("href"))
```

```Python
import pandas as pd

# Looking for the 'id' attribute with a value of ten_years_first
table = soup.find("table", attrs={"id": "ten_years_first"})

heading_table = []  # List where the names of the columns will be stored

# Find all <th> elements in the table and run them through in a loop
for row in table.find_all('th'):
	# Add the content from the <th> tag to the heading_table list using append()
    heading_table.append(row.text) 

print(heading_table) # ["Ship's Name", "Shipwreck Date", "Shipwreck Location"]


content = []  # list where the table data will be stored
# Each row is wrapped in a <tr> tag, we need to loop through all the rows
for row in table.find_all('tr'):
    # Condition to ignore the first row of the table, with headings
    if not row.find_all('th'):
	    # Loop through all <td> elements, extract the content from the cells, &            add it to the list; add each of the lists to the content list
        content.append([element.text for element in row.find_all('td')])

print(content)


# Create a Pandas DF, by passing two-dimensional content list as data and heading_table as headings
shipwrecks = pd.DataFrame(content, columns=heading_table)
```

#### `select_one()`
* Searches through a file and returns the FIRST instance that matches the CSS-selector criteria 
	* Arguments
		* `selector=` -- the CSS-selector to be used; can search for a 
			* tag selector
			* id-selector
			* class-selector
```Python
# Example - using the selector() method

# Selecting the FIRST instance of an <a> tag inside a <p> tag
company_url = soup.select_one(selector="p a")
print(company_url)

# Selecting the FIRST instance where an ID is 'name'
name = soup.select_one(selector="#name")
print(name)

# Selecting the FIRST isntances where the class name is 'heading'
soup.select_one(".heading")
```

#### `select()`
 * Searches through a file and returns the ALL instances that matches the CSS-selector criteria 
	* Arguments
		* `selector=` -- the CSS-selector to be used; can search for a 
			* tag selector
			* id-selector
			* class-selector
```Python
# Selecting ALL instances of an anchor tag inside a paragraph tag
company_url = soup.select_one(selector="p a")
print(company_url)

# Selecting ALL instances where an ID is 'name'
name = soup.select_one(selector="#name")
print(name)

# Selecting all isntances where the class name is 'heading'
soup.select(".heading")
print(heading_all)
```

#### `get()`
* Gets a specified element's attribute
	* Arguments
		* `element` -- the element to be used when retrieving the value
```Python
# Example -- Using the get() Method

# Accessing the FIRST item with an <h3> tag and a class of 'heading'
section_heading = soup.find(name="h3", class_="heading")

# Getting the value of the 'class' in the section_heading variable
print(section_heading.get("class"))
```

```Python
# Example -- Using the get() Method

# Accessing ALL items with an <a> tag
all_anchor_tags = soup.find_all(name="a")

# Getting the value of the href attribute
for tag in all_anchor_tags:
	print(tag.get("href"))
```

```Python
# Example -- Using the get() Method

form_tag = soup.find("input")
max_length = form_tag.get("maxlength")
```

#### `getText()`
* Gets the text from an element
	* Arguments
		* `text` -- the text to be extracted 
```Python
# Example -- Using the getText() Method
all_anchor_tags = soup.find_all(name="a")

# Getting the text from the tag variable
for tag in all_anchor_tags:
	print(tag.getText())
```



---
# Examples:
1. Extracting info from website & creating a DataFrame with it
```Python
import pandas as pd
import requests  
from bs4 import BeautifulSoup 

URL = 'https://store.data-analyst.praktikum-services.ru/en/'
req = requests.get(URL)  
soup = BeautifulSoup(req.text, 'lxml')

name_products = []  # List where the product names are stored
for row in soup.find_all('div', attrs={'class': 't754__title t-name t-name_md'}):
    name_products.append(row.text)

price = []  # List where the product prices are stored
for row in soup.find_all('div', attrs={'class': 't754__price-value js-product'}):
    price.append(row.text)

# DataFrame with the data on product names and prices
products_data = pd.DataFrame({'name': name_products, 'price': price})
print(products_data.head(5))
```