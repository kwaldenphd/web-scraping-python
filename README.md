# Data Scraping in Python

<a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license"><img style="border-width: 0;" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" alt="Creative Commons License" /></a>
This tutorial is licensed under a <a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license">Creative Commons Attribution-NonCommercial 4.0 International License</a>.

## Lab Overview

This lab provides an introduction and overview to parsing HTML in Python using the `beautiful soup` package.

## Acknowledgements

The author consulted the following materials when building this lab:
- Lisa Tagliaferri, "How to Scrape Web Pages With Beautiful Soup and Python 3" *Digital Ocean* (20 March 2019). https://www.digitalocean.com/community/tutorials/how-to-scrape-web-pages-with-beautiful-soup-and-python-3
- Jeri Wieringa, "Intro to Beautiful Soup," *The Programming Historian* 1 (2012), https://doi.org/10.46430/phen0008.
- Martin Breuss, "Beautiful Soup: Build a Web Scraper With Python" *Real Python*. https://realpython.com/beautiful-soup-web-scraper-python/
- DataQuest, "Tutorial: Web Scraping With Python Using Beautiful Soup" *DataQuest* (2 September 2020). https://www.dataquest.io/blog/web-scraping-tutorial-python/

The introductory sections of this lab are based on and adapted from:
- Lisa Tagliaferri, "How to Scrape Web Pages With Beautiful Soup and Python 3" *Digital Ocean* (20 March 2019). https://www.digitalocean.com/community/tutorials/how-to-scrape-web-pages-with-beautiful-soup-and-python-3

# Table of Contents

- [Introduction to Beautiful Soup](#introduction-to-beautiful-soup)
- [Installing Beautiful Soup](#installing-beautiful-soup)
- [Loading URLs in Python](#loading-urls-in-python)
- [Creating a Beautiful Soup Object](#creating-a-beautiful-soup-object)
- [Identifying HTML Tables](#identifying-html-tables)
- [More Adventures in Reading Technical Documentation](#more-adventures-in-reading-technical-documentation)
  * [What is Digital Ocean](#what-is-digital-ocean)
  * [Digital Ocean's Education Community](#digital-oceans-education-community)
- [File Methods in Python](#file-methods-in-python)
- [Additional Lab Notebook Questions](#additional-lab-notebook-questions)
- [Lab Notebook Questions](#lab-notebook-questions)

[Link to lab notebook template](https://docs.google.com/document/d/1_bbenDLXoWf6N-ZPZrjTvWUcCjPCoCayxv1AyQDR2qU/copy) (Google Doc, ND users)

# Introduction to Beautiful Soup

1. What is Beautiful Soup? 

2. "Beautiful Soup is a Python library for pulling data out of HTML and XML files. It works with your favorite parser to provide idiomatic ways of navigating, searching, and modifying the parse tree. It commonly saves programmers hours or days of work" ([Beautiful Soup Documentation](https://www.crummy.com/software/BeautifulSoup/bs4/doc/))

3. The library name is an allusion to the song Lewis Carroll character the Mock Turtle sings in Chapter 10 of *Alice's Adventures in Wonderland*.

4. `Beautiful Soup` uses the structure of markup language documents (i.e. HTML, XML, etc) to extract information we can work with in a Python programming environment.

5. In this lab, we will be focusing on using `Beautiful Soup` to parse and scrape web pages built using HTML and CSS.

# Installing Beautiful Soup

6. We can install `Beautiful Soup` at the command line using a terminal or shell in our Python environment.

7. To install `Beautiful Soup` using `pip`:
- `pip install beautifulsoup4`

8. For more on installing modules using `pip`: Fred Gibbs, "Installing Python Modules with pip," The Programming Historian 2 (2013), https://doi.org/10.46430/phen0029.

9. We also can install the `lxml` library to help with parsing HTML.

10. To install `lxml` using `pip`:
- `pip install lxml`

# Loading URLs in Python

11. We will be using the `requests` library to load URLs in Python.

12. This library is already built into Python and does not require additional installation.

13. Core syntax for using the `requests` library to load a URL:

```Python
# import requests
import requests

# load url using get requests.get() method
page = requests.get('URL GOES HERE')
```

# Creating a Beautiful Soup Object

14. Once we have a URL loaded in Python, we want to be able to use `BeautifulSoup` to parse the web page's HTML components.

15. We can do that by creating a BeautifulSoup object.

16. Core syntax:

```Python
# import beautifulsoup
from bs4 import BeautifulSoup

# create beautifulsoup object
soup = BeautifulSoup(page.text, 'html.parser')
```

17. Putting that all together, the core syntax for loading a URL and creating a BeautifulSoup object:

```Python
# import requests
import requests

# import beautifulsoup
from bs4 import BeautifulSoup

# load url using get requests.get() method
page = requests.get('URL GOES HERE')

# create beautiful soup object
soup = BeautifulSoup(page.text, 'html.parser')
```

18. Now, we are ready to parse the web page's HTML using `BeautifulSoup`.

# Identifying HTML Tables

<blockquote>This section of the lab focuses on the tags used to create tables in an HTML document. If you are not familiar with HTML (hyper-text markup language) syntax, a couple of resources that can get you started:
 <ul>
  <li><a href="https://www.w3schools.com/html/">W3 Schools HTML Tutorial</a></li>
  <li><a href="https://www.w3schools.com/css/">W3 Schools CSS Tutorial</a></li>
 </ul>
 </blockquote>
 
19. HTML uses a few core tags for web pages that include tables.
- `table` (marks the start and end of a table
- `tbody` (marks the start and end of the table body)
- `tr` (marks the start and end of each table row)
- `th` (marks the start and end of each column in the first row of the table)
- `td` (marks the start and end of each column after the first row of the table)

20. How we might see those tags combined in a table structure:

```HTML
<table>
 <tr>
  <th>First Column Header</th>
  <th>Second Column Header</th>
  <th>Third Column Header</th>
 </tr>
 <tr>
  <td>Data in first column/first row</td>
  <td>Data in second column/first row</td>
  <td>Data in third column/first row</td>
 </tr>
 <tr>
  <td>Data in first column/second row</td>
  <td>Data in second column/second row</td>
  <td>Data in third column/second row</td>
 </tr>
</table>
```

21. The output of that HTML would look like:

<table>
 <tr>
  <th>First Column Header</th>
  <th>Second Column Header</th>
  <th>Third Column Header</th>
 </tr>
 <tr>
  <td>Data in first column/first row</td>
  <td>Data in second column/first row</td>
  <td>Data in third column/first row</td>
 </tr>
 <tr>
  <td>Data in first column/second row</td>
  <td>Data in second column/second row</td>
  <td>Data in third column/second row</td>
 </tr>
</table>

22. Additional attributes like `align`, `style`, etc. can be used with many of these tags.

# More Adventures in Reading Technical Documentation

23. Rather than work through a lab procedure that includes step-by-step instructions and guidance designed for students in this class, we're going to get some experience using an online  tutorial written for a general audience.

24. Tutorial we will be using: Lisa Tagliaferri, "How to Scrape Web Pages With Beautiful Soup and Python 3" *Digital Ocean* (20 March 2019). https://www.digitalocean.com/community/tutorials/how-to-scrape-web-pages-with-beautiful-soup-and-python-3

25. Open the Digital Ocean ["How to Scrape Web Pages With Beautiful Soup and Python 3"](https://www.digitalocean.com/community/tutorials/how-to-scrape-web-pages-with-beautiful-soup-and-python-3) tutorial in another browser window.

## What is Digital Ocean?

26. "DigitalOcean, Inc. is an American cloud infrastructure provider headquartered in New York City with data centers worldwide. DigitalOcean provides developers cloud services that help to deploy and scale applications that run simultaneously on multiple computers" ([Wikipedia](https://en.wikipedia.org/wiki/DigitalOcean))

27. DigitalOcean was founded in 2011 and was part of TechStar's 2012 startup accelerator program.

28. Initial rounds of funding came from IA Ventures, the Fortress Investment Group, Access Industries, and Andreessen Horowitz.

29. The company's IPO took place in March 2021.

## Digital Ocean's Education Community

30. In additional to commercial products and enterprise solutions, DigitalOcean includes robust community forums and staff members dedicated to writing [open educational resources](https://www.digitalocean.com/community/tutorials), like the tutorial we'll be using.

31. This tutorial was written by [Dr. Lisa Tagliaferri](https://twitter.com/lisaironcutter), who worked as member of the company's Community and Education team before starting as [Sourcegraph's](https://t.co/aQZBLY1hhK?amp=1) Director of Developer Education in February 2021.

32. The Digital Ocean tutorial walks through scraping data from National Gallery of Art web pages that include artist names and biographical information.

<blockquote>Q1: Include code + comments that document your experience working through the Digital Ocean tutorial.</blockquote>

<blockquote>Q2: Reflect on your experience working through the Digital Ocean tutorial. What challenges did you face? How did you approach or solve them? How was this experience different than previous labs?</blockquote>

33. Additional tutorials you are welcome to consult as needed:
- Jeri Wieringa, "Intro to Beautiful Soup," *The Programming Historian* 1 (2012), https://doi.org/10.46430/phen0008.
- Martin Breuss, "Beautiful Soup: Build a Web Scraper With Python" *Real Python*. https://realpython.com/beautiful-soup-web-scraper-python/
- DataQuest, "Tutorial: Web Scraping With Python Using Beautiful Soup" *DataQuest* (2 September 2020). https://www.dataquest.io/blog/web-scraping-tutorial-python/

# File Methods in Python

33. One of the final steps in the DigitalOcean tutorial is saving the extracted or scraped content to a CSV file.

34. Before you work with BeautifulSoup on your own, let's talk more about how Python handles creating, reading, and writing files.

35. Specifically, we will be focusing on a few key Python functions for working with files.
- `open()`
- `write()`

## `open()`

36. The `open()` function lets us open an existing file or create a new file in Python.

37. For either version of `open()` (new file or existing file), we need to specify the file name (with the file type extension) and access mode.

38. Core syntax for opening an existing file:

```Python
open(file_name.extension, access_mode)
```

39. The file type extension is the string of characters that follows the period after the file name.

40. Examples include `.py`, `.csv`, `.txt`, etc.

41. The types of file handling functions we are covering in this lab will generally only support reading and writing plain-text (or machine-readable) files.

## Access Modes

42. The access mode parameter specifies the types of modifications that can be made to the file. It can also specify the type of data or information contained in the file.

43. Possible access mode parameters:

<table>
 <tr>
  <th>Parameter</th>
  <th>Name</th>
  <th>Description</th>
 </tr>
 <tr>
  <td><code>"r"</code></td>
  <td>Read</td>
  <td>Opens a file for reading; also the default value</td>
 </tr>
 <tr>
  <td><code>"a"</code></td>
  <td>Append</td>
  <td>Opens the file for appending new or additional information; Creates the file if it does not already exist</td>
 </tr>
 <tr>
  <td><code>"w"</code></td>
  <td>Write</td>
  <td>Opens the file for writing new information; Creates the file if it does not already exist</td>
 </tr>
 <tr>
  <td><code>"x"</code></td>
  <td>Create</td>
  <td>Creates the file if it does not already exist</td>
 </tr>
 </table>

44. Additionally, we can specify the type of data contained in the file, or how Python should handle the information in the file.

<table>
 <tr>
  <th>Parameter</th>
  <th>Name</th>
  <th>Description</th>
 </tr>
 <tr>
  <td><code>"t"</code></td>
  <td>Text</td>
  <td>Treats file as text data; also the default value</td>
 </tr>
 <tr>
  <td><code>"b"</code></td>
  <td>Binary</td>
  <td>Treats the file as binary data</td>
 </tr>
 </table>
 
 ### `open()` examples
 
 ```Python
 # opens an existing text (TXT) file with overwrite permission
 f = open("existing_file.txt", "w")
 ```
 
 ```Python
 # opens an existing CSV file and reads the content
 f = open("existing_file.csv", "r")
 ```
 
 ```Python
 # creates new txt file with write permission
 f = open("new_file.txt", "w")
 ```
 
 ```Python
 # creates new CSV file without write privileges
 f = open("new_file.csv", "x")
 ```
 
45. If you these examples, you will see a newly-created file appear in your environment or project workspace. 

## `write()`

46. Now that we have a newly-created file in Python, we can use the `write()` function to ***write*** content to that file.

47. Let's say we want to create a `.txt` (plain text) file and write a string to that file.

48. We can do that using `write()`.

49. An example:

```Python
# creates new txt file with write permission
f = open("new_file.txt", "w")

# writes string to new file
f.write("Hello world!")

# closes file
f.close()
```

50. NOTE: It is ***very important*** to `close()` the file once you are done writing content or making modifications.

51. Another example where we have assigned a string to a variable and write the variable to the `.txt` file:

```Python
# creates new txt file with write permission
f = open("new_file.txt", "w")

# assigns string to variable
hello_world = "Hello world!"

# writes string variable to new file
f.write(hello_world)

# closes file
f.close()
```

52. Open the `new_file.txt` file to see the newly-added content.

53. For more on file handling methods in Python:
- [Python File Handling, W3Schools](https://www.w3schools.com/python/python_file_handling.asp)
- [Python File Write, W3Schools](https://www.w3schools.com/python/python_file_write.asp)
- [Python open() Function](https://www.w3schools.com/python/ref_func_open.asp)

## `open()`, `write()`, and `CSV` files

54. In the Digital Ocean tutorial, we are taking artist names and biographical information and writing that to a `CSV` file.

55. `CSV` stands for comma-separated values.

56. `CSV` files are the plain-text, machine-readable file type for tabular data (table data, or data in a spreadsheet structure)

57. For example, a table that looks like this in a spreadsheet program like Excel or Google Sheets:
<table>
 <tr>
  <th>Parameter</th>
  <th>Name</th>
  <th>Description</th>
 </tr>
 <tr>
  <td><code>"t"</code></td>
  <td>Text</td>
  <td>Treats file as text data; also the default value</td>
 </tr>
 <tr>
  <td><code>"b"</code></td>
  <td>Binary</td>
  <td>Treats the file as binary data</td>
 </tr>
 </table>

58. Would look like this as a CSV:

```CSV
Parameter, Name, Description
"t", Text, Treats file as text data; also the default value
"b", Binary, Treats the file as binary data
```

59. So when writing data to a `CSV` file, we need Python to understand the row structure and comma-separated syntax for the file type.

60. Specifically, we need Python to understand we are writing individual rows of data to the file, and we need Python to understand that those rows consist of columns of data separated by columns.

### The CSV Module

61. Thankfully, Python has a built-in [`CSV` module](https://docs.python.org/3/library/csv.html) with specialized functions designed to help with writing `CSV` files.

#### A Quick Detour Into Packages, Modules, and Libraries

62. We're now starting to encounter language like `package`, `module`, and `library` when working in Python.

63. All of these terms refer to external Python programs that we can use in our program without having to recreate the entire original code.

64. We can think of these resources as "expansion packs" for Python that expand or extend the programming language's built-in functionality.

65. A few preliminary definitions...

66. A ***module*** is a Python file that typically includes specialized functions and variables. 
- Modules typically have `.py` file extensions.

67. A single or simple directory of modules is called a ***package***. 
- Packages are typically a simple directory with multiple modules.
- They include an `__init__.py` file that provides additional details on how to initialize the package and access its modules.
- Packages can also contain sub-packages

68. A ***library*** includes blocks of code that can be reused within a program. Libraries are a collection of modules.
- Libraries can include methods we call using period-method name (`.method_name()`)
- They have a much more complex directory/sub-directory/etc structure than packages

69. Some modules, packages, and libraries are built-in to Python and require no additional installation.

70. Others have to be installed (typically at the command line, or in the terminal) before you can import and use them in a program.

#### Back to the `CSV` Module

71. We'll spend a lot more time with the `CSV` module in a future lab.

72. For now, we'll focus on how we can use the module to create and write `CSV` files.

73. We can create a file using the `open()` function covered in a previous section of the lab.

```Python
 # create new CSV file with write privileges
 f = open("new_file.csv", "w")
 ```
 
74. The next step is to create the `writer` object using the `csv.writer()` function.

```Python
# create writer object
outputWriter = csv.writer(f)
```

75. Next, we can use the `.writerow()` method to write individual lists as rows in our `CSV` file.

```Python
# write first row
outputWriter.writerow(['Parameter', 'Name', 'Description')]

# write second row
outputWriter.writerow(['t', 'Text', 'Treats file as text data; also the default value'])

# write third row
outputWriter.writerow(['b', 'Binary', 'Treats the file as binary data')]
```

76. After we have finished writing new rows of data, we can close the file.

```Python
f.close()
```

77. Putting that all together:

```Python
 # create new CSV file with write privileges
 f = open("new_file.csv", "w")
 
 # create writer object
outputWriter = csv.writer(f)

# write first row
outputWriter.writerow(['Parameter', 'Name', 'Description')]

# write second row
outputWriter.writerow(['t', 'Text', 'Treats file as text data; also the default value'])

# write third row
outputWriter.writerow(['b', 'Binary', 'Treats the file as binary data')]

# close file
f.close()
```

78. Check out `new_file.csv` to see the newly-created file with rows of data.

#### `.writerow()`, loops, and `BeautifulSoup`

79. The next lab notebook question (Q3) asks you to write a Python program that scrapes data from a webpage and saves it to a plain-text file.

80. Depending on the website you choose and the type of data you are working with, you may end up in a situation where you need to find multiple instances of an HTML tag on a web page and write each of those instances to a row in your newly-created CSV file.

81. If only there was a way we could iterate through each instance of a specific HTML tag and run `.writerow()` on the contents of that tag....

82. Enter `for` loops! 

83. We can use a `for` loop in combination with `.writerow()` to iterate through a list of items or objects, do *something* with each object, and write that output to a CSV file.

84. This workflow becomes especially helpful when working with `BeautifulSoup`.

85. For example, say you have a webpage with a list of links, and you want to extract the URLs and text for each link as a new row in a CSV file.

86. First, we can use the `.find_all()` method within `BeautifulSoup` to have Python find all instances of a specific element or tag.

```Python
# import requests
import requests

# import beautifulsoup
from bs4 import BeautifulSoup

# load url using get requests.get() method
page = requests.get('URL GOES HERE')

# create beautiful soup object
soup = BeautifulSoup(page.text, 'html.parser')

# create new CSV file with write access
f = csv.writer(open('new_file.csv', 'w'))

# write header row or first row for CSV file
f.writerow(['Link_Text', 'URL'])

# find all instances of the a tag (a href) and assign those instances to a list called "links"
links = soup.find_all('a')
```

87. Then, we can use a `for` loop to instruct Python to perform specific `BeautifulSoup` operations on each item in our list, and write that output as a row in the CSV file.
```Python
for link in links:
 SOMETHING WILL HAPPEN HERE
```

88. To get the text for each link:
```Python
names = link.contents
```

89. To get the URL for each link:
```Python
fullLink = link.get('href')
```

90. And write both values as a row in our CSV file:
```Python
f.writerow([names, fullLink])
```

91. And we can put all of those steps together in a `for` loop:
```Python
for link in links:
 names = link.contents[0]
 fullLink = link.get('href')
 f.writerow([names, fullLink])
```

92. That whole combined program:
```Python
# import requests
import requests

# import beautifulsoup
from bs4 import BeautifulSoup

# load url using get requests.get() method
page = requests.get('URL GOES HERE')

# create beautiful soup object
soup = BeautifulSoup(page.text, 'html.parser')

# create new CSV file with write access
f = csv.writer(open('new_file.csv', 'w'))

# write header row or first row for CSV file
f.writerow(['Link_Text', 'URL'])

# find all instances of the a tag (a href) and assign those instances to a list called "links"
links = soup.find_all('a')

# for loop that extracts link text and url and writes to CSV file
for link in links:
 names = link.contents[0]
 fullLink = link.get('href')
 f.writerow([names, fullLink])

# close file 
f.close()
```

93. How exactly you combine `BeautifulSoup` and `CSV` module functions with a `for` loop depends on what you are wanting to scrape from a web page as well as the desired output or structure for the file you are creating.

# Additional Lab Notebook Questions

Q3: Select a web page of your choosing and write a Python program that downloads select content from that web page as a CSV or TXT file. That content could be paragraphs of text, tables of data, etc. Include code + comments.

Some websites that can get you started (although you are not restricted to these resources).

Websites for unstructured text:
- [Wikisource](https://en.wikisource.org/wiki/Main_Page)
- [Project Gutenberg](https://www.gutenberg.org/)
- [HathiTrust Digital Library](https://www.hathitrust.org/) 
  * Click the `Login` button in the top-right hand corner and select the University of Notre Dame to log in with your Notre Dame credentials.

Websites for structured data:
- [Wikipedia](https://en.wikipedia.org/wiki/Main_Page)
  * Some pages (especially for athletic teams or competitions) will have tables of data. For example, check out this Wikipedia page on the [Summer Olympic Games](https://en.wikipedia.org/wiki/All-time_Olympic_Games_medal_table).
- Other Sport Data Sources
  * [KenPom ratings](https://kenpom.com/)
  * [Her Hoop Stats](https://herhoopstats.com/)
  * [Hockey DB](https://www.hockeydb.com/)

Q4: Reflect on your experience tackling Q3 (and this lab more generally):
- What are some of your main takeaways from this lab?
- How you think the concepts/skills covered in this lab might be useful in other contexts or for future projects?
- What challenges did you face for Q3? How did you approach and/or solve them?
- Any other comments/observations

This lab notebook can be submitted as a Jupyter Notebook (code + reflection) or a `.py` file with additional reflection text document.

# Lab Notebook Questions

[Link to lab notebook template](https://docs.google.com/document/d/1_bbenDLXoWf6N-ZPZrjTvWUcCjPCoCayxv1AyQDR2qU/copy) (Google Doc, ND users)

Q1: Include code + comments that document your experience working through the Digital Ocean tutorial.

Q2: Reflect on your experience working through the Digital Ocean tutorial. What challenges did you face? How did you approach or solve them? How was this experience different than previous labs?

Q3: Select a web page of your choosing and write a Python program that downloads select content from that web page as a CSV or TXT file. That content could be paragraphs of text, tables of data, etc. Include code + comments.

Some websites that can get you started (although you are not restricted to these resources).

Websites for unstructured text:
- [Wikisource](https://en.wikisource.org/wiki/Main_Page)
- [Project Gutenberg](https://www.gutenberg.org/)
- [HathiTrust Digital Library](https://www.hathitrust.org/) 
  * Click the `Login` button in the top-right hand corner and select the University of Notre Dame to log in with your Notre Dame credentials.

Websites for structured data:
- [Wikipedia](https://en.wikipedia.org/wiki/Main_Page)
  * Some pages (especially for athletic teams or competitions) will have tables of data. For example, check out this Wikipedia page on the [Summer Olympic Games](https://en.wikipedia.org/wiki/All-time_Olympic_Games_medal_table).
- Other Sport Data Sources
  * [KenPom ratings](https://kenpom.com/)
  * [Her Hoop Stats](https://herhoopstats.com/)
  * [Hockey DB](https://www.hockeydb.com/)

Q4: Reflect on your experience tackling Q3 (and this lab more generally):
- What are some of your main takeaways from this lab?
- How you think the concepts/skills covered in this lab might be useful in other contexts or for future projects?
- What challenges did you face for Q3? How did you approach and/or solve them?
- Any other comments/observations

This lab notebook can be submitted as a Jupyter Notebook (code + reflection) or a `.py` file with additional reflection text document.
