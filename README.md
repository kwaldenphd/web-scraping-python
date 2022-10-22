# Web Scraping in Python

<a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license"><img style="border-width: 0;" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" alt="Creative Commons License" /></a>
This tutorial is licensed under a <a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license">Creative Commons Attribution-NonCommercial 4.0 International License</a>.

## Lab Overview

This lab provides an introduction and overview to parsing HTML in Python using `beautifulsoup` and `pandas`.

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=c49fc924-268d-4f3b-a0cc-ade900293029">Lab overview</a></td>
  </tr>
  </table>
  
<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?pid=134db1ac-7685-4fce-b121-adea01531389">Lecture/live coding playlist</a></td>
  </tr>
  </table>
  
## Acknowledgements

The author consulted the following materials when building this lab:
- Lisa Tagliaferri, "How to Scrape Web Pages With Beautiful Soup and Python 3" *Digital Ocean* (20 March 2019). https://www.digitalocean.com/community/tutorials/how-to-scrape-web-pages-with-beautiful-soup-and-python-3
- Jeri Wieringa, "Intro to Beautiful Soup," *The Programming Historian* 1 (2012), https://doi.org/10.46430/phen0008.
- Martin Breuss, "Beautiful Soup: Build a Web Scraper With Python" *Real Python*. https://realpython.com/beautiful-soup-web-scraper-python/
- DataQuest, "Tutorial: Web Scraping With Python Using Beautiful Soup" *DataQuest* (2 September 2020). https://www.dataquest.io/blog/web-scraping-tutorial-python/

The introductory sections of this lab are based on and adapted from:
- Lisa Tagliaferri, "How to Scrape Web Pages With Beautiful Soup and Python 3" *Digital Ocean* (20 March 2019). https://www.digitalocean.com/community/tutorials/how-to-scrape-web-pages-with-beautiful-soup-and-python-3

# Table of Contents

- [Lecture & Live Coding](#lecture--live-coding)
- [Lab Notebook Template](#lab-notebook-template)
- [Overview](#overview)
- [Beautiful Soup](#beautiful-soup)
  * [Introduction to Beautiful Soup](#introduction-to-beautiful-soup)
  * [Installing Beautiful Soup](#installing-beautiful-soup)
  * [Loading URLs in Python](#loading-urls-in-python)
  * [Creating a Beautiful Soup Object](#creating-a-beautiful-soup-object)
- [Beautiful Soup & Structured Data](#beautiful-soup--structured-data)
  * [Concept Refresh](#concept-refresh)
    * [HTML Refresh](#html-refresh)
    * [File Methods Refresh](#file-methods-refresh)
  * [Using BeautifulSoup with a Single Web Page](#using-beautifulsoup-with-a-single-web-page)
    * [Sample For Loops](#sample-for-loops)
  * [Working With Multiple Pages](#working-with-multiple-pages)
- [An Alternate Approach: `pandas.read_html()`](#an-alternate-approach-pandasread_html)
- [Beautiful Soup & Unstructured Text](#beautiful-soup---unstructured-text)
  * [Oh, the Places You Could Go](#oh-the-places-you-could-go) 
- [Why did we do this?](#why-did-we-do-this)
- [Lab Notebook Questions](#lab-notebook-questions)
- [Final Project Next Steps](#final-project-next-steps)

[Link to lab procedure as a Jupyter Notebook]()

# Lecture & Live Coding

Throughout this lab, you will see a Panopto icon at the start of select sections.

This icon indicates there is lecture/live coding asynchronous content that accompanies this section of the lab. 

You can click the link in the figure caption to access these materials (ND users only).

Example:

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=c49fc924-268d-4f3b-a0cc-ade900293029">Lab overview</a></td>
  </tr>
  </table>
  
<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?pid=134db1ac-7685-4fce-b121-adea01531389">Lecture/live coding playlist</a></td>
  </tr>
  </table>

# Lab Notebook Template

Lab notebook template:
- [Jupyter Notebook](https://drive.google.com/file/d/1LRsbOC11-8YrPUNBJNAzJDiIM_CQJ3go/view?usp=sharing)

# Overview

INTRO TO WEB SCRAPING, WHY ARE WE DOING THIS

# Beautiful Soup

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=ab460bfe-4adc-40a4-8072-ade9002b5fa6">Getting Started With Beautiful Soup</a></td>
  </tr>
  </table>
  
## Introduction to Beautiful Soup

What is Beautiful Soup? "Beautiful Soup is a Python library for pulling data out of HTML and XML files. It works with your favorite parser to provide idiomatic ways of navigating, searching, and modifying the parse tree. It commonly saves programmers hours or days of work" ([Beautiful Soup Documentation](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)) The library name is an allusion to the song Lewis Carroll character the Mock Turtle sings in Chapter 10 of *Alice's Adventures in Wonderland*.

`Beautiful Soup` uses the structure of markup language documents (i.e. HTML, XML, etc) to extract information we can work with in a Python programming environment. In this lab, we will be focusing on using `Beautiful Soup` to parse and scrape web pages built using HTML and CSS.

## Installing Beautiful Soup

We'll need to install a couple of libraries to be able to parse HTML with `BeautifulSoup`
- `BeautifulSoup`: `pip install beautifulsoup4`
- `lxml`: `pip install lxml`

## Loading URLs in Python

We will be using the `requests` library to load URLs in Python. This library is already built into Python and does not require additional installation. Core syntax for using the `requests` library to load a URL:

```Python
# import requests
import requests

# load url using get requests.get() method
page = requests.get('URL GOES HERE')
```

## Creating a Beautiful Soup Object

Once we have a URL loaded in Python, we want to be able to use `BeautifulSoup` to parse the web page's HTML components. We can do that by creating a BeautifulSoup object. Core syntax:

```Python
# import beautifulsoup
from bs4 import BeautifulSoup

# create beautifulsoup object
soup = BeautifulSoup(page.text, 'html.parser')
```

Putting that all together, the core syntax for loading a URL and creating a BeautifulSoup object:

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

Now, we are ready to parse the web page's HTML using `BeautifulSoup`.

# Beautiful Soup & Structured Data

## Concept Refresh

### HTML Refresh

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=1ed9a128-e2f1-4415-a8ea-ade9002f2f98">HTML Refresh</a></td>
  </tr>
  </table>
  
When using `BeautifulSoup`, we can isolate information on the webpage through interacting with the HTML syntax. HTML uses a few core tags for web pages that include tables.
- `table` (marks the start and end of a table
- `tbody` (marks the start and end of the table body)
- `tr` (marks the start and end of each table row)
- `th` (marks the start and end of each column in the first row of the table)
- `td` (marks the start and end of each column after the first row of the table)

How we might see those tags combined in a table structure:

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

The output of that HTML would look like:

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

Additional attributes like `align`, `style`, etc. can be used with many of these tags. Some other tags that we might encounter when trying to parse HTML using `BeautifulSoup`:

<table>
    <tr>
        <td>Name</td>
        <td>Syntax</td>
        <td>Description</td>
    </tr>
    <tr>
        <td>Heading</td>
        <td><code>h1, h2, h3, etc</code></td>
            <td>HTML headings</td>
            </tr>
            <tr>
                <td>Division</td>
                <td><code>div</code></td>
                <td>Defines sections or divisions in an HTML document</td>
            </tr>
            <tr>
                <td>Paragraph</td>
                <td><code>p</code></td>
                <td>Defines paragraphs in an HTML document</td>
            </tr>
            <tr>
                <td>Span</td>
                <td><code>span</code></td>
                <td>Defines a section in an HTML document</td>
            </tr>
            <tr>
                <td>Unordered list</td>
                <td><code>ul</code></td>
                <td>Defines the start of an unordered list (followed by <code>li</code> tags)</td>
            </tr>
            <tr>
                <td>Hyperlink</td>
                <td><code>a</code></td>
                    <td>Defines a hyperlink in an HTML document (followed by <code>href = "URL"</code>)</td>
            </tr>
            </table>


For more detail on HTML and CSS:
- [W3Schools HTML Tutorial](https://www.w3schools.com/html)
- [W3Schools CSS Tutorial](https://www.w3schools.com/css)
- [EoC HTML/CSS Lab](https://github.com/kwaldenphd/HTML-CSS/tree/EoC1-F20)

### File Methods Refresh

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=1ed9a128-e2f1-4415-a8ea-ade9002f2f98">File Methods Refresh</a></td>
  </tr>
  </table>

As part of our work in this lab, we'll be saving the content we have scraped from a web page to a plain-text file (either `.txt` or `.csv`). A quick review of how Python handles creating, reading, and writing files, specifically focusing on...
- `open()`
- `write()`

#### `open()`

The `open()` function lets us open an existing file or create a new file in Python. For either version of `open()` (new file or existing file), we need to specify the file name (with the file type extension) and access mode.

```Python
 # creates new txt file with write permission
 f = open("new_file.txt", "w")
```
 
```Python
 # creates new CSV file with write privileges
 f = open("new_file.csv", "w")
```

[Click here](https://github.com/kwaldenphd/python-structured-data#file-io--access-modes) To review file I/O and access modes in Python.
 
#### `write()`

Once we have a newly-created file in Python, we can use the `write()` function to ***write*** content to that file.

```Python
# creates new txt file with write permission
f = open("new_file.txt", "w")

# writes string to new file
f.write("Hello world!")

# closes file
f.close()
```

Another example where we have assigned a string to a variable and write the variable to the `.txt` file:

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

#### `open()`, `write()`, and `.csv` files

A quick review:
- `CSV` stands for comma-separated values.
- `CSV` files are the plain-text, machine-readable file type for tabular data (table data, or data in a spreadsheet structure)

An overview of the workflow for creating a CSV file using the `csv` module:
- Create a file using the `open()` function
- Create the `writer` object using the `writer()` function.
- Use the `.writerow()` method to write individual lists as rows

Putting that all together:

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

## Using BeautifulSoup With a Single Web Page

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=c33c1d07-578e-464b-85ac-ade900316fc1">BeautifulSoup and a Single Web page</a></td>
  </tr>
  </table>

Now, we're going to see HTML syntax and file methods at work to develop a web scraping program that takes tabular data on a web page and writes it to a `CSV` file. 

### Finding a Table

Head to https://en.wikipedia.org/wiki/All-time_Olympic_Games_medal_table in a web browser. There are a nubmer of tables on this page, but we're going to focus on the `Unranked medal table (sortable)` section of the page.

<p align="center"><img src="https://github.com/kwaldenphd/web-scraping-python/blob/main/images/fig1.jpg?raw=true"></p>

Take a look at this table on the public web page, thinking about the rows, columns, and data values we might want to map onto a tabular (table, spreadsheet) data structure.

<p align="center"><img src="https://github.com/kwaldenphd/web-scraping-python/blob/main/images/fig2.jpg?raw=true"></p>

Then, right click on the page (`Control-click` on a Mac) and select the `View Page Source` option.
- The specific label for this option may differ across browsers and operating systems.

<p align="center"><img src="https://github.com/kwaldenphd/web-scraping-python/blob/main/images/fig3.jpg?raw=true"></p>

There's a lot going on here- we're looking at the back-end HTML for the Wikipedia page with the table we want to work with. But we want to figure out what HTML elements are adjacent to the section of the page we want to isolate. Scrolling through the HTML until you see things that look promising is one place to start. You can also type `Control-F` (`Command-F` on a Mac) to search for particular words/phrases in the HTML. We know one of the country names in the table is `Afghanistan`, so let's search the HTML to see where that term appears.

```HTML
<th style="width:2em;">
<p><span title="Combined total number of all Medals won by each country" class="rt-commentedText" style="border-bottom:1px dotted">Total</span>
</p>
</th></tr>
<tr>
<td align="left"><span id="AFG"><img alt="" src="//upload.wikimedia.org/wikipedia/commons/thumb/c/cd/Flag_of_Afghanistan_%282013%E2%80%932021%29.svg/22px-Flag_of_Afghanistan_%282013%E2%80%932021%29.svg.png" decoding="async" width="22" height="15" class="thumbborder" srcset="//upload.wikimedia.org/wikipedia/commons/thumb/c/cd/Flag_of_Afghanistan_%282013%E2%80%932021%29.svg/33px-Flag_of_Afghanistan_%282013%E2%80%932021%29.svg.png 1.5x, //upload.wikimedia.org/wikipedia/commons/thumb/c/cd/Flag_of_Afghanistan_%282013%E2%80%932021%29.svg/44px-Flag_of_Afghanistan_%282013%E2%80%932021%29.svg.png 2x" data-file-width="900" data-file-height="600" />&#160;<a href="/wiki/Afghanistan_at_the_Olympics" title="Afghanistan at the Olympics">Afghanistan</a>&#160;<span style="font-size:90%;">(AFG)</span></span>
</td>
<td style="background:#f2f2ce;">15</td>
<td style="background:#f2f2ce;">0</td>
<td style="background:#f2f2ce;">0</td>
<td style="background:#f2f2ce;">2</td>
<td style="background:#f2f2ce;">2
</td>
<td style="background:#cedff2;">0</td>
<td style="background:#cedff2;">0</td>
<td style="background:#cedff2;">0</td>
<td style="background:#cedff2;">0</td>
<td style="background:#cedff2;">0
</td>
<td>15</td>
<td>0</td>
<td>0</td>
<td>2</td>
<td>2
</td></tr>
<tr>
```

Again, there's still a lot going on, but we can see the table row `<tr>` tag around a section of HTML that includes multiple `<td>` tags with information about the country name (`Afghanistan`) and number values that correspond to the medal counts from that row in the table. Now, we need to figure out where this table "starts," or what HTML elements mark the beginning/end of the table. If we scroll up from the `Afghanistan` search results, we can see the section of HTML that marks the start of this table.

```HTML
<h2><span id="Unranked_medal_table_.28sortable.29"></span><span class="mw-headline" id="Unranked_medal_table_(sortable)">Unranked medal table (sortable)</span><span class="mw-editsection"><span class="mw-editsection-bracket">[</span><a href="/w/index.php?title=All-time_Olympic_Games_medal_table&amp;action=edit&amp;section=1" title="Edit section: Unranked medal table (sortable)">edit</a><span class="mw-editsection-bracket">]</span></span></h2>
<p>The table is pre-sorted by the name of each Olympic Committee, but can be displayed as sorted by any other column, such as the total number of <a href="/wiki/Gold_medal" title="Gold medal">gold medals</a> or total number of overall medals. To sort by gold, silver, and then bronze, sort first by the bronze column, then the silver, and then the gold. The table does not include revoked medals (e.g., due to <a href="/wiki/Doping_in_sport" title="Doping in sport">doping</a>).
</p><p>Medal totals in this table are current through the <a href="/wiki/2020_Summer_Olympics" title="2020 Summer Olympics">2020 Summer Olympics</a> in <a href="/wiki/Tokyo" title="Tokyo">Tokyo</a>, Japan, and all <a href="/wiki/List_of_stripped_Olympic_medals" title="List of stripped Olympic medals">changes in medal standings</a> due to doping cases and medal redistributions up to 8 August 2021 are taken into account.
</p>
<style data-mw-deduplicate="TemplateStyles:r981673959">.mw-parser-output .legend{page-break-inside:avoid;break-inside:avoid-column}.mw-parser-output .legend-color{display:inline-block;min-width:1.25em;height:1.25em;line-height:1.25;margin:1px 0;text-align:center;border:1px solid black;background-color:transparent;color:black}.mw-parser-output .legend-text{}</style><div class="legend"><span class="legend-color" style="background-color:lightblue; color:black;">&#160;</span>&#160;Special delegation, not an actual nation</div> 
<table class="wikitable sortable" style="margin-top:0; text-align:center; font-size:90%;">

<tbody><tr>
<th>Team
</th>
<th align="center" style="background-color:#f2f2ce;" colspan="5"><a href="/wiki/Summer_Olympic_Games" title="Summer Olympic Games">Summer Olympic Games</a>
</th>
<th align="center" style="background-color:#cedff2;" colspan="5"><a href="/wiki/Winter_Olympic_Games" title="Winter Olympic Games">Winter Olympic Games</a>
</th>
<th align="center" colspan="5"><a href="/wiki/Olympic_Games" title="Olympic Games">Combined total</a>
</th></tr>
<tr>
<th><span title="International Olympic Committee country code" class="rt-commentedText" style="border-bottom:1px dotted">Team (IOC&#160;code)</span>
</th>
```

Since we're looking for a table, identifying a `<table>` tag is a good place to start. We can see the line `<table class="wikitable sortable" style="margin-top:0; text-align:center; font-size:90%;">` marks the start of the medal count table. This gives us the critical pieces of information we need when working in Python with `BeautifulSoup` to isolate this section of HTML.
 
### Load URL & Create BeautifulSoup Object

The first step in our program is to import the libraries we'll need, load the web page using `requests` and create the `BeautifulSoup` object.

```Python
# import statements
import requests
from bs4 import BeautifulSoup
import csv
import pandas as pd
```

```Python
# get page
page = requests.get("https://en.wikipedia.org/wiki/All-time_Olympic_Games_medal_table")

# create BeautifulSoup object
soup = BeautifulSoup(page.text, 'html.parser')

# show BeautifulSoup object
soup
```

At this point we have loaded the web page into Python as a `BeautifulSoup` object.

### Extract Medal Table

The next step is to use `BeautifulSoup` to identify and isolate the section of the web page we want to focus on. We can do this using the `.find()` or `.find_all()` with our `BeautifulSoup` object.
- `.find()` isolates a single instance of an HTML class or tag
- `.find_all()` creates a list-like object with each instance of a specific tag or class

```Python
# basic syntax for find
soup.find("HTML TAG  GOES HERE")

# a specific example with the p tag
soup.find("p")
```

```Python
# basic syntax for find_all, this time using a class instead of a tag
soup.find_all(class_ = "CLASS NAME GOES HERE")

# a specific example using the wikitable sortable class
soup.find_all(class_ = 'wikitable sortable')
```

Again, we know the line of HTML `<table class="wikitable sortable" style="margin-top:0; text-align:center; font-size:90%;">` marks the start of the medal count table. But we don't know how many instances of the `<table>` tag or `wikitable sortable` class appear in this web page. Some more work with `Command-F`/`Control-F` shows us there are 30 instances of the `<table>` tag and 9 instances of the `wikitable sortable` class in this page. So let's use `.find_all()` with the `wikitable sortable` class and then figure out which of those 9 instances is the table we want to work with.

```Python
# isolate all HTML with wikitable sortable class
tables = soup.find_all(class_ = 'wikitable sortable')
```

Then, we can use index operators to go through the items in `tables` to see which one has the HTML we want to work with.

```Python
# show first table in tables
tables[0]
```

The first table in the list is the medal count, so we can assign that to a variable.

```Python
# isolate first table in tables
table = tables[0]
```

Now that we have just the HTML for the table we want to work with, we want to create a list-like object for each row in the table. So, we can use `.find()` or `.find_all()` again to create a list-like object with all elements that match a particular class or tag. In this case, we want the HTML for each row in the table to be a value or element in the list, so we're going to be looking for the table row `<tr>` tag. And since this table has multiple rows, we're going to use `.find_all("tr")` to find all instances of the `<tr>` tag and map those onto a list-like structure.

```Python
# get all table rows from medal_table
rows = table.find_all("tr")

# show table rows
rows
```

### Testing On Single Table Row (Single Country)

So now we have the HTML for each row in the table as a list value in our `medal_test` list. To recap:
- Load url using `requests.get()` 
- Creat `BeautifulSoup` object using `BeautifulSoup()
- Isolate section of page with table using `.find_all()` (with `wikitable sortable` class) and index values
- Create list of rows using `.find_all()` (with `tr` tag)

We'll eventually want to figure out how to iterate over all the rows in the table, but for now, let's isolate a single row so we can test our program on a single row. Since the first two rows in the the table have column header information and do not match the structure/format of the country rows, we'll use the third row (first country row) for our single-row testing.

```Python
# isolate first country in medal_table
row = rows[2]

# show first country
row
```

Now, we have a `row` object that includes the entire HTML associated with the `<tr>` tag for `Afghanistan`. As before, we want to create a list-like object for each cell or column in the table. Since there are multiple cells in each row, we'll use `.find_all()` to look for the table cell `<td>` tag and map those values onto a list-like structure.

```Python
# get all cells in single_country
cells = row.find_all("td")

# show single country
cells
```

Now we have a list of cells (`<td>` tags) for a single row of HTML in the original table. The next step is to figure out how we work within that list of `<td>` tag contents to isolate the specific values we want to eventually write to each row in our `.csv` file. At this point, before we start writing code to extract these values, it's useful to stop and think about the endpoint for the data scraping process. Specifically, thinking about what columns we have in mind for the ultimate data structure helps us keep the end goal in mind as we start working through each aspect of the program.

For this table, we might want a data structure with the following columns:
- `Country_Name`
- `Country URL`
- `Number of Summer Olympic Appearances`
- `Number of Summer Olympic Gold Medals`
- `Number of Summer Olympic Silver Medals`
- `Number of Summer Olympic Bronze Medals`
- `Total Number of Summer Olympic Medals`
- `Number of Winter Olympic Appearances`
- `Number of Winter Olympic Gold Medals`
- `Number of Winter Olympic Silver Medals`
- `Number of Winter Olympic Bronze Medals`
- `Total Number of Winter Olympic Medals`
- `Combined Number of Olympic Appearances`
- `Combined Number of Gold Medals`
- `Combined Number of Silver Medals`
- `Combined Number of Bronze Medals`
- `Total Combined Number of Medals`

So let's figure out how we can isolate each of those values, with the ultimate goal of developing a program that can iterate over all the similarly-structured rows in our table.

#### Country Name

To get the country name, we can isolate the first cell (`<td>` tag) in the `row` list of cells.

```Python
# isolate first cell in single_country
country_name = cells[0]

# show first cell
country_name
```

Then, we can use `.contents[]` (part of `BeautifulSoup`) to get the contents of that first cell.

```Python
# isolate country name using contents and index
name = cells.contents[0]

# show country_name HTML
name
```

So now we have the HTML associated with the first `<td>` tag, but there's still a lot of extraneous markup we want to remove to get just the country name.

```HTML
<span id="AFG"><img alt="" class="thumbborder" data-file-height="600" data-file-width="900" decoding="async" height="15" src="//upload.wikimedia.org/wikipedia/commons/thumb/c/cd/Flag_of_Afghanistan_%282013%E2%80%932021%29.svg/22px-Flag_of_Afghanistan_%282013%E2%80%932021%29.svg.png" srcset="//upload.wikimedia.org/wikipedia/commons/thumb/c/cd/Flag_of_Afghanistan_%282013%E2%80%932021%29.svg/33px-Flag_of_Afghanistan_%282013%E2%80%932021%29.svg.png 1.5x, //upload.wikimedia.org/wikipedia/commons/thumb/c/cd/Flag_of_Afghanistan_%282013%E2%80%932021%29.svg/44px-Flag_of_Afghanistan_%282013%E2%80%932021%29.svg.png 2x" width="22"/> <a href="/wiki/Afghanistan_at_the_Olympics" title="Afghanistan at the Olympics">Afghanistan</a> <span style="font-size:90%;">(AFG)</span></span>
```

If we drill down into this HTML, we can see the `<a href...>` tag is the HTML element closest to the country name we want to extract. So let's use `.find()` to get just the `a` tag HTML.

```Python
# get HTML with a tag
name = name.find('a')

# show name_tag
name
```

Now with just the `a` tag (`<a href="/wiki/Afghanistan_at_the_Olympics" title="Afghanistan at the Olympics">Afghanistan</a>`), we can use `.contents[]` again to get the tag contents. Remember an index value goes in the brackets for `.contents[]`.

```Python
# get contents of a href tag
name = name.contents[0]

# show country
name
```

Voila! The country name. Putting that all together:

```Python
# combined program for country name
name = cells.contents[0].find('a').contents[0]
```

### Country URL

```HTML
<span id="AFG"><img alt="" class="thumbborder" data-file-height="600" data-file-width="900" decoding="async" height="15" src="//upload.wikimedia.org/wikipedia/commons/thumb/c/cd/Flag_of_Afghanistan_%282013%E2%80%932021%29.svg/22px-Flag_of_Afghanistan_%282013%E2%80%932021%29.svg.png" srcset="//upload.wikimedia.org/wikipedia/commons/thumb/c/cd/Flag_of_Afghanistan_%282013%E2%80%932021%29.svg/33px-Flag_of_Afghanistan_%282013%E2%80%932021%29.svg.png 1.5x, //upload.wikimedia.org/wikipedia/commons/thumb/c/cd/Flag_of_Afghanistan_%282013%E2%80%932021%29.svg/44px-Flag_of_Afghanistan_%282013%E2%80%932021%29.svg.png 2x" width="22"/> <a href="/wiki/Afghanistan_at_the_Olympics" title="Afghanistan at the Olympics">Afghanistan</a> <span style="font-size:90%;">(AFG)</span></span>
```

If we look at the HTML associated with `country_name`, we can see that the country's Wikipedia URL is also in this section of HTML, as part of the `<a href...>` tag. So we can again use `.find()` to isolate the `<a>` tag's contents.

```Python
# get first/only instance of a link tag in HTML for single country
link = name.find('a')

# show link
link
```

Now, looking at the `link_test` piece of HTML (`<a href="/wiki/Afghanistan_at_the_Olympics" title="Afghanistan at the Olympics">Afghanistan</a>`), we want to extract the URL associated with the `href` attribute. We were able to use `.contents[]` to get the contents of this HTML tag, but we'll need a different approach for getting the `href` attribute value. `BeautifulSoup` includes a `.get()` argument that lets us isolate the value associated with an HTML attribute. So we can use `.get('href')` to isolate the URL.

```Python
# get the contents of the url from the href attribute
link = link.get('href')

# show href contents
link
```

But wait! `/wiki/Afghanistan_at_the_Olympics` doesn't look like a full url...That's because it isn't. Wikipedia is using an internal link with the `<a href...>` tag to connect to another Wikipedia page, which means they don't have to use the full URL for the link to work. But, we can use concatenation to recreate the full link, since all English-language Wikipedia pages start with the same root URL: `https://en.wikipedia.org`

```Python
# use contenation to get full url
link = "https://en.wikipedia.org" + link

# show full link
link
```

Great! Now we have the full link.

```Python
# combined program for link
link = name.find('a').get('href')
link = "https://en.wikipedia.org" + link
```

#### Medal Counts

If we take a look at the original Wikipedia table, we notice there are three column "groupings":
- `Summer Olympic Games`
- `Winter Olympic Games`
- `Combined total`

We can extract medal counts within each of these column groups by selecting the cell and then getting the value of that cell using `contents[]` and index values.

```Python
# number of summer olympic appearances
summer = cells[1].contents[0]

# number of summer gold medals
summer_gold = cells[2].contents[0]

# number of summer silver medals
summer_silver = cells[3].contents[0]

# number of summer bronze medals
summer_bronze = cells[4].contents[0]

# total number of summer olympics medals, using strip() to remove line break
summer_medals = cells[5].contents[0].strip()

# total number of winter olympic appearances
winter = cells[6].contents[0]

# number of winter gold medals
winter_gold = cells[7].contents[0]

# number of winter silver
winter_silver = cells[8].contents[0]

# number of winter bronze
winter_bronze = cells[9].contents[0]

# total number of winter medals
winter_medals = cells[10].contents[0].strip()

# total number combined olympic appearances
combined_olympics = cells[11].strip()

# total number gold medals
gold_total = cells[12].contents[0]

# total number silver medals
silver_total = cells[13].contents[0]

# total number bronze medals
bronze_total = cells[14].contents[0]

# total number of medals, combined
medals_total = cells[15].contents[0].strip()

# create list with all of these values
medals = [summer, summer_gold, summer_silver, summer_bronze, summer_medals, winter, winter_gold, winter_silver, winter_bronze, winter_medals, combined_olympics, gold_total, silver_total, bronze_total, medals_total]

# show list
print(medals)
```

We could also create a list with the medal data and the country names + links we extracted in the previous section of the lab.

```Python
# add country name and URL to medals list
medals.insert(country_name, 0)
medals.insert(link, 1)

# show updated list
print(medals)
```

Now we have working code that extracts each piece of data from a row in the table.

### Iterating Over Multiple Rows

To recap our workflow so far:
- Load url using `requests.get()` 
- Creat `BeautifulSoup` object using `BeautifulSoup()
- Isolate section of page with table using `.find_all()` (with `wikitable sortable` class) and index values
- Create list of rows using `.find_all()` (with `tr` tag)
- Isolate single row using index values
- Develop program that works on single row using combination of index values, `.get()`, `.find()`, and `.contents[]`
- Create list from extracted values


Now that we have working code that will extract each piece of data as a variable, we want to run these lines of code on each country in the table to get the data in each column. We can do this using a `for` loop that iterates over each row in the table. 

But before we throw iteration into the mix, we might want to remove or exclude rows in the table that don't follow the pattern or structure of the rows with data. Specifically for this table, the first two rows have the column header information and don't match the format/structure of the rest of the table. One option for removing these rows would be `del` statements.

```Python
# remove second row
del rows[1]

# remove first row
del rows[0]

# show updated list of rows
print(rows)
```

Alternate workflow that uses list comprehension to subset `rows`:

```Python
# recreate list of rows
rows = table.find_all('tr')

# subset rows to drop first two
index_list = [0, 1]

# use list comprehension to subset list
rows = [rows[i] for i in index_list]

# show updated list of rows
rows
```

<blockquote>For more on list comprehension: https://www.w3schools.com/python/python_lists_comprehension.asp</blockquote>

Now we're ready to iterate over each country (table row) using the code we tested on a single country. We can create a list with each row's values and append that list as a sublist or nested list to an empty list.

```Python
table_rows = [] # empty list for data

for row in table: # for loop that iterates over rows
	tags = [] # create empty list for td tags in single row
	
	cells = row.find_all('td') # isolate cells, td elements
	
	tags.append(cells) # append tags to tag list
	
	for cells in tags: # for loop that iterates over cells in row
		try:
			name = cells.contents[0].find('a').contents[0] # name
			link = name.find('a').get('href') # link
			link = "https://en.wikipedia.org" + link
			summer = cells[1].contents[0] # number of summer olympic appearances
			summer_gold = cells[2].contents[0] # number of summer gold medals
			summer_silver = cells[3].contents[0] # number of summer silver medals
			summer_bronze = cells[4].contents[0] # number of summer bronze medal
			summer_medals = cells[5].contents[0].strip() # total number of summer olympics medals, using strip() to remove line break
			winter = cells[6].contents[0] # total number of winter olympic appearances
			winter_gold = cells[7].contents[0] # number of winter gold medals
			winter_silver = cells[8].contents[0] # number of winter silver
			winter_bronze = cells[9].contents[0] # number of winter bronze
			winter_medals = cells[10].contents[0].strip() # total number of winter medals
			combined_olympics = cells[11].strip() # total number combined olympic appearances
			gold_total = cells[12].contents[0] # total number gold medals
			silver_total = cells[13].contents[0] # total number silver medals
			bronze_total = cells[14].contents[0] # total number bronze medals
			medals_total = cells[15].contents[0].strip() # total number of medals, combined

            		# creates list of values from each data element
            		row_data = [name, link, summer, summer_gold, summer_silver, summer_bronze, summer_medals, winter, winter_gold, winter_silver, winter_bronze, winter_medals, combined_olympics, gold_total, silver_total, bronze_total, medals_total]

            		# append row_data to test_list
            		table_rows.append(row_data)
            
        	except:
            		continue
    
# show list
table_rows
```

Each row of data in the table is a list value, or sublist/nested list in `tags`. In this program `try` and `except` instruct Python to `try` to run the lines nested under `try`, but if it runs into an error (`except`), `continue` iterating over the values in the `tags` list. Using `try` and `except` can be dangerous if you don't know if or how a program is working- in this case, we've tested the program and got it working on a single row that matches the pattern for all the rows we want to scrape data frame.

Now that we know the iteration is working, we can take `table_rows` and write each item in the list (which itself is a row of data) to a row in a `.csv` file.

```Python
# create new csv file
f = csv.writer(open('medals.csv', 'w'))

# list of strings with headers
headers = ["country_name", "link", "no_summer_olympics", "no_summer_gold", "no_summer_silver", "no_summer_bronze", "total_no_summer_medals", "no_winter_olympics", "no_winter_gold", "no_winter_silver", "no_winter_bronze", "total_no_winter_medals", "no_combined_olympics", "no_combined_gold", "no_combined_silver", "no_combined_bronze", "total_no_combined_medals"]

# write header row or first row for CSV file
f.writerow(headers)

# for loop that assigns each element in test_list to a new row
for row in table_rows:
    f.writerow(row)
```

We can also use `table_rows` and `headers` to create a `pandas` `DataFrame`. `pandas` will map each value in the list (nested list or sublist with single row of data) to a row in the `DataFrame`. And the `headers` list we created for writing the first row of the `medals` CSV file can be used to set the `DataFrame` column names.

```Python
# import pandas
import pandas as pd

# list of strings with headers
headers = ["country_name", "link", "no_summer_olympics", "no_summer_gold", "no_summer_silver", "no_summer_bronze", "total_no_summer_medals", "no_winter_olympics", "no_winter_gold", "no_winter_silver", "no_winter_bronze", "total_no_winter_medals", "no_combined_olympics", "no_combined_gold", "no_combined_silver", "no_combined_bronze", "total_no_combined_medals"]

# create data frame 
df = pd.DataFrame(table_rows, columns=headers)

# show df
df
```

Then we could use `pd.to_csv` to write the `DataFrame` to a `CSV` file.

```Python
# write df to csv file
df.to_csv("output.csv", index=False)
```

## Application

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=81459156-8f91-4897-8af4-ade9004561f8">Lab Notebook Questions 1-5</a></td>
  </tr>
  </table>

Q1: Describe the general approach to loading a web page in Python using `requests` and isolating the section of HTML you need using `BeautifulSoup`. What are the basic steps involved in this workflow, thinking about what happens at the start of the program to isolate the section of HTML you would need to do further work with to extract the data you want to work with?

Q2A: Select another Wikipedia page that includes a table. From looking at the public web page, what data do you want to scrape from this web page (i.e. specific table, multiple tables, etc.)? What do you want the resulting data structure to look like (columns, rows, etc)?

Q2B: Take a look at the HTML for this page. What tags or other HTML components do you see around the section of the page you want to work with? For this question, we're thinking about how we will end up writing a program with <code>BeautifulSoup</code> to isolate a section of the web page.

Q2C: Develop an outline for a Python program that scrapes data from the web page you selected. 

A preliminary workflow:
- Load URL and create BeautifulSoup object
- Isolate section of HTML with your table (either directly or extract from list)
- Isolate table row elements (create list where each element is a table row)
- Extract contents from row (isolate the pieces of information from each row)
- Create Pandas DataFrame
- Write extracted row contents to CSV file

NOTE: You do not need to have working code for all components of this program. That's where we're heading with the final project. At this point, we're focusing on the conceptual framework for the web scraping program. Start to build out code where you can, but think about the programming version of outlining a paper.

Q2D: What challenges or roadblocks did you face working on Q4? What parts of the program do you understand/feel ready to develop at this point? What parts of the program are less clear?

# Working With Multiple Pages

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=86675173-9734-4f0f-8a06-ade900486927">Working With Multiple Pages</a></td>
  </tr>
  </table>

In the previous example of a Wikipedia page with Olympic medal counts, we were scraping data from a single web page. But we can also imagine a scenario where we might want to scrape data from multiple web pages or a series of web pages that have the same HTML structure or format. For example, head to https://www.sports-reference.com/cfb/schools/notre-dame/1940-schedule.html to explore the College Football Reference page for Notre Dame's 1940 football season.

<p align="center"><img src="https://github.com/kwaldenphd/web-scraping-python/blob/main/images/fig4.jpg?raw=true"></p>

We can use the `Previous Year` and `Next Year` buttons at the top of the page to look at pre- and post-1940 pages. Take a look at page URLs as you change years- the start (or root) of the url `https://www.sports-reference.com/cfb/schools/notre-dame/` and the end (or tag) of the url `-schedule.html` remain the same, while only the year value changes. Since the data format/structure is fairly consistent across the different season pages, if we get a program working for one season/page, it stands to reason we could run that program on multiple pages by iterating over a list of URLs.

Let's take a look at how we could get a list of URLs programmatically for the College Football Reference Notre Dame pages. First, we would assign the URL root and tag to named variables.

```Python
# root url
root = "https://www.sports-reference.com/cfb/schools/notre-dame/"

# url tag
tag = "-schedule.html"
```

Then, we could use `range` to create a list of years spanning the dates we want to cover.

```Python
# year range
years = list(range(1899, 2021, 1))
```

Then, we could use concatenation and a `for` loop to generate a list of full URLs for the seasons we want to cover.

```Python
# empty list for urls
urls = []

# for loop that concatenates full url
for year in years:
    urls.append(root + str(year) + tag)
    
# show list of urls
urls
```

With the `urls` list, we could write a program that works for a single page and then use a `for` loop to iterate over each url in the `urls` list.

Putting that all together:

```Python
root = "https://www.sports-reference.com/cfb/schools/notre-dame/"

years = list(range(1899, 2021, 1))

tag = "-schedule.html"

urls = []

for year in years:
    urls.append(root + str(year) + tag)
    
urls
```

### Application

Q3: Describe in your own words how the url generation program covered in the previous section of the lab works. The full program is also included below. What is happening in the different program components?

Q4: Select another Sports Reference web page that follows this pattern and write a program that generates a list of full URLs for that team/organization.

A few places to start:
- Baseball Reference season web pages have the following URL pattern:
  * `https://www.baseball-reference.com/teams/`, `TEAM ABBREVIATION`, `SEASON`, `.shtml`
- Basketball Reference season web pages have a similar pattern for NBA teams:
  * `https://www.basketball-reference.com/teams/`, `TEAM ABBREVIATION`, `SEASON`, `.html`
- Basketball Reference uses a slightly different pattern for its WNBA pages:
  * `https://www.basketball-reference.com/wnba/teams`, `TEAM ABBREVIATION`, `SEASON`, `.html`
- College Basketball Reference pages also follow a pattern: 
  * `https://www.sports-reference.com/cbb/schools`, `SCHOOL ABBREVIATION`, `SEASON`, `.html`
- For Hockey Reference pages: 
  * `https://www.hockey-reference.com/teams/`, `TEAM ABBREVIATION`, `SEASON`, `.html`
- Football Reference pages follow the same pattern for men's and women's teams:
  * `https://fbref.com/en/squads/`, `SQUAD ID`, `SEASON`, `TEAM NAME`
- Pro Football Reference pages also have a pattern: 
  * `https://www.pro-football-reference.com/teams/`, `TEAM ABBREVIATION`, `SEASON`, `.htm`

NOTE: You DO NOT need to write a program that scrapes data from these pages for this question. The purpose of this question is to be able to programmatically generate a list of URLs that cover a date range. 

# An Alternate Approach: pandas.read_html()

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=94cac193-ae03-43e8-890e-ade9004d9a17">pandas.read_html()</a></td>
  </tr>
  </table>

`BeautifulSoup` is an incredibly powerful package that lets us drill down into the structure of an HTML document to isolate the pieces of information we need or want to work with. But if we're dealing with an HTML table that has straightforward formatting, an alternate approach is to use the `.read_html()` function that is part of the `pandas` library. `pd.read_html()` looks for any `<table>` tag on a web page and reads each `<table>`  tag's HTML into Python as a list of `DataFrame` objects. Let's take a look at how we could use `pd.read_html()` for the College Football Reference web page we looked at in the previous section of the lab.

```Python
# import pandas
import pandas as pd

# load url
url = "https://www.sports-reference.com/cfb/schools/notre-dame/1940-schedule.html"

# create list of dataframes from url using .read_html()
dfs = pd.read_html(url)

# show dfs list
dfs
```

We could also the URL directly to `pd.read_html()`:

```Python
# import pandas
import pandas as pd

# create list of dataframes from url using .read_html()
dfs = pd.read_html("https://www.sports-reference.com/cfb/schools/notre-dame/1940-schedule.html")

# show dfs list
dfs
```

At first glance, `dfs` doesn't seem to have clear data tables, but remember `dfs` is a list of `DataFrames` created from any HTML `table` content on the page.

```Python
# number of elements in dfs list
len(dfs)
```

Since there are only two elements in the `dfs` list, let's isolate each one.

```Python
# show first dataframe in dfs
dfs[0]
```

These values correspond to the `AP Poll Summary` table on the page.

```Python
# show second dataframe in dfs
dfs[1]
```

These values correspond to the `9 Games` schedule table on the page. We could create a single `DataFrame` by selecting the second element in `dfs`.

```Python
# select single dataframe 
df = dfs[1]

# show new dataframe
df
```

College Football Reference schedule pages for pre-1936 Notre Dame do not have the first `AP Poll` table. We can use the 1935 schedule page (https://www.sports-reference.com/cfb/schools/notre-dame/1935-schedule.html) as an example.

```Python
# load url
url = "https://www.sports-reference.com/cfb/schools/notre-dame/1935-schedule.html"

# create list of dataframes from url using .read_html()
dfs = pd.read_html(url)

# show number of tables in dfs
len(dfs)
```

Only one table here, so we can isolate that table as a `DataFrame`.

```Python
# select single dataframe 
df = dfs[0]

# show new dataframe
df
```

If we were ultimately going to do further work with analyzing/visualizing this data, we would probably want to spend some more time standardizing column names and values. And if we were going to scrape this table across multiple pages, we would need to find some way to get the year or season represented in the `DataFrame`. But for now, if we wanted to write the `DataFrame` we created using `pd.read_html()` to a `CSV`...

```Python
df.to_csv("output.csv", index=False)
```

## Application

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=73a9d3b1-4a1e-4923-ae1c-ade900503cb8">Lab Notebook Questions 8-11</a></td>
  </tr>
  </table>
  
Q5: Describe the general approach to loading a web page in Python using `pd.read_html()`. What are the basic steps involved in this workflow, thinking about what happens to identify/isolate the specific table you want to work with?

Q6: For Q4, you generated a list of Sports Reference URLs covering a time span for a specific team/organization. Select three years and web pages from that list- something early in the time period covered, something in the middle of the time period covered, and something toward the end of the time period covered. Do these pages have the same pattern in terms of number and order of tables? For one of these pages, what table or tables on these pages would you want to be able to extract and work with?

Q7A: Develop an outline for a Python program that uses `pd.read_html()` to scrape data from one of the web pages you select in Q6.

A preliminary workflow:
- Use `pd.read_html()` to create a list of DataFrame objects
- Identify which DataFrame object in the list is the table you want to work with
- Isolate the list element to create a new DataFrame
- Write the new DataFrame to a CSV file

NOTE: For Q3, you did not need to have working code for all components of this program. Since `pd.read_html()` has an easier learning curve, let's see if we can flesh out more of this program. But if you run into problems, it's okay to focus on the conceptual framework for the web scraping program. Start to build out code where you can, but think about the programming version of outlining a paper.

ANOTHER NOTE: For many Sports Reference pages, tables further down the page are buried in HTML comments. These tables will not show up when you use `pd.read_html()`. We can come back to these "hidden tables" in the final project, but for now, focus on the tables that do show up when you use `pd.read_html()`.

Q7B: What challenges or roadblocks did you face working on Q10? What parts of the program do you understand and/or were able to develop? What parts of the program are less clear?

# `Beautiful Soup` & Unstructured Text

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=8218edd5-5c66-4f2e-9fe6-ade90052aa96">Unstructured Text</a></td>
  </tr>
  </table>

So far, this lab has focused on approaches for scraping structured data from the web using Python. But there are other contexts and use cases when we might want to be able to scrape unstructured text from the web and be able to work with that "data" in Python (or write it to a plain-text `.txt` file). For example, take a look at Fall 2021 *Observer* article: https://web.archive.org/web/20211016150109/https://ndsmcobserver.com/2021/10/south-bend-community-leaders-discuss-role-of-notre-dame-in-fight-for-black-civil-rights/

Imagine we wanted to use Python to analyze the words or terms used in this article. The first step would be to get a plain-text `.txt` version of the article text.  We would start with the same `BeautifulSoup` workflow we've used previously:
- Load URL
- Create `BeautifulSoup` object
- Isolate section of HTML with article text

```Python
# get page
page = requests.get("https://web.archive.org/web/20211016150109/https://ndsmcobserver.com/2021/10/south-bend-community-leaders-discuss-role-of-notre-dame-in-fight-for-black-civil-rights/")

# create BeautifulSoup object
soup = BeautifulSoup(page.text, 'html.parser')

# show BeautifulSoup object
soup
```
Next, we want to isolate the section of the page that includes the article text.

```HTML
<article class="section news">
<div class="title-container">
<h2 class="topic"><span class="title">news</span></h2>
<ul class="see-social addthis_toolbox" addthis:url="https://ndsmcobserver.com/2021/10/south-bend-community-leaders-discuss-role-of-notre-dame-in-fight-for-black-civil-rights/" addthis:title="South Bend community leaders discuss role of Notre Dame in fight for Black civil rights" addthis:description="South Bend community leaders discuss role of Notre Dame in fight for Black civil rights">
<li><a class="addthis_button_email email"></a></li>
<li><a class="addthis_button_facebook facebook"></a></li>
<li><a class="addthis_button_twitter twitter"></a></li>
</ul> 
</div> 
<div class="content-header">
<h3>South Bend community leaders discuss role of Notre Dame in fight for Black civil rights</h3>
<p class="info"><a href="https://web.archive.org/web/20211016150109/https://ndsmcobserver.com/author/vortiz2/" title="Posts by Valeria Ortiz" class="author url fn" rel="author">Valeria Ortiz</a> | Friday, October 15, 2021</p>

</div> 
<span id="outstream-unit" style="width:100%;height:550px;padding:0.5em 0"></span>
<div class="content-body">
<p>The Notre Dame Initiative on Race and Resilience hosted a panel Wednesday in DeBartolo Hall on Black civil rights in South Bend, featuring some of South Bend’s prominent community leaders.</p>
<p>The panel, which intended to explore the immense social inequalities facing South Bend’s Black residents, included Trina Robinson, president of NAACP-South Bend; Regina Williams-Preston, president of Community Action for Education and former South Bend Common Council representative; Jorden Giger, co-founder of Black Lives Matter South Bend and Deacon Mel Tardy, deacon of St. Augustine Parish and an advising faculty at the University.</p>
<figure id="attachment_234452" class="wp-caption aligncenter" style="width: 700px"> <div class="media-credit-container aligncenter" style="max-width: 710px">
<img data-attachment-id="234452" data-permalink="https://web.archive.org/web/20211016150109/https://ndsmcobserver.com/2021/10/south-bend-community-leaders-discuss-role-of-notre-dame-in-fight-for-black-civil-rights/screen-shot-2021-10-15-at-8-36-39-pm/" data-orig-file="https://web.archive.org/web/20211016150109/https://i1.wp.com/ndsmcobserver.com/wp-content/uploads/2021/10/1634330204-71900895f520822.png?fit=726%2C538&amp;ssl=1" data-orig-size="726,538" data-comments-opened="1" data-image-meta="{&quot;aperture&quot;:&quot;0&quot;,&quot;credit&quot;:&quot;&quot;,&quot;camera&quot;:&quot;&quot;,&quot;caption&quot;:&quot;&quot;,&quot;created_timestamp&quot;:&quot;0&quot;,&quot;copyright&quot;:&quot;&quot;,&quot;focal_length&quot;:&quot;0&quot;,&quot;iso&quot;:&quot;0&quot;,&quot;shutter_speed&quot;:&quot;0&quot;,&quot;title&quot;:&quot;&quot;,&quot;orientation&quot;:&quot;0&quot;}" data-image-title="Screen Shot 2021-10-15 at 8.36.39 PM" data-image-description="" data-medium-file="https://web.archive.org/web/20211016150109/https://i1.wp.com/ndsmcobserver.com/wp-content/uploads/2021/10/1634330204-71900895f520822.png?fit=700%2C519&amp;ssl=1" data-large-file="https://web.archive.org/web/20211016150109/https://i1.wp.com/ndsmcobserver.com/wp-content/uploads/2021/10/1634330204-71900895f520822.png?fit=700%2C519&amp;ssl=1" class="wp-image-234452 size-medium" src="https://web.archive.org/web/20211016150109im_/https://i1.wp.com/ndsmcobserver.com/wp-content/uploads/2021/10/1634330204-71900895f520822.png?resize=700%2C519&amp;ssl=1" alt="" width="700" height="519" srcset="https://web.archive.org/web/20211016150109im_/https://i1.wp.com/ndsmcobserver.com/wp-content/uploads/2021/10/1634330204-71900895f520822.png?resize=700%2C519&amp;ssl=1 700w, https://web.archive.org/web/20211016150109im_/https://i1.wp.com/ndsmcobserver.com/wp-content/uploads/2021/10/1634330204-71900895f520822.png?w=726&amp;ssl=1 726w" sizes="(max-width: 700px) 100vw, 700px" data-recalc-dims="1"/><span class="media-credit">Valeria Ortiz | The Observer</span> </div>
<figcaption class="wp-caption-text">In a Wednesday panel, community activists encouraged the University to give to local Black-owned businesses to support inclusion and business growth.</figcaption></figure>
<p>The panelists offered their experiences and recommendations toward a stronger future for civil rights within the local community. They called for action to combat systemic racism — a historical pattern of denying opportunity to fair education, health and housing opportunities in South Bend.</p>
<p>“He who wins the war gets to tell the story, so now we believe it all right. Here we are today seeing how that history gets uncovered,” Williams-Preston said.</p>
<p>For more than a century, Tardy explained, African Americans have been moving to the north with the intention of looking for jobs after the Great Migration.</p>
<p>“We have about 27% of [the] African American population,” Tardy said.</p>
<p>However, the promise of labor has quickly shifted to the lack of job opportunities for people of color.</p>
<p>“A lot of the families are having difficulty getting places to stay where there is some sort of consistency,” Tardy said.</p>
<p>As mentioned in the panel, South Bend’s eviction rate is three times the national average. Low wages, prejudiced state policies and lack of affordable housing are the three main explanations for the city’s drastic increase in evictions, Williams Preston explained — and many citizens being displaced are people of color.</p>
<p>In addition to the struggles people of color face in finding jobs, Robinson said the systematic racism that exists won’t let these communities break out of that endless loop of neglect.</p>
<p>Panelists then discussed the ongoing disparities in the racial education gap, agreeing that the first step in improving the system is acknolwedging that there is an issue: Systematic racism leads to academic underperformance in children of color.</p>
<p>“There exists a systematic problem … Black children don’t have less capabilities; the system is against them,” Williams-Preston said.</p>
<p>Tardy emphasized the importance of educational resources and of having a strong focus on elementary schools where foundational skills are taught, such as reading and writing. He also stressed increasing accessibility of mental health resources.</p>
<p>Robinson spoke of the need for reliable institutions in the education system.</p>
<p>“We should hold corporations accountable for educating our children and for acknowledging the things that are not working,” Robinson said.</p>
<p>Black-owned businesses struggle to grow because of the lack of support from big institutions and Indiana’s state government, Williams-Preston said.</p>
<p>“It’s killing us,” she said.</p>
<p>Williams-Preston said young people of color, including students, entrepreneurs and members of the community, are leaving South Bend due to a lack of opportunity.</p>
<p>There is also space for improvement in the community of Notre Dame in eradicating “nepotism and favoritism,” Williams-Preston said. She argued that Notre Dame should support Black community efforts in “mining [their] gold” from the Westside Black communities in order to make them feel more connected.</p>
<p>Panelists also suggested efforts to improve cooperation between local businesses and Notre Dame, including direct funding from the University in supporting local small Black-owned businesses. Efforts such as these, Williams-Preston explained, would provide much-needed space for business growth, talent training and inclusion within the community.</p>
<p>“If we can do that, we won’t even be the first, but that’s the kind of thing Notre Dame needs to invest in &#8230; committing to becoming a leader in this community by investing in cooperative businesses right here at home,” Williams-Preston said.</p>
<span class="tags">Tags: <a href="https://web.archive.org/web/20211016150109/https://ndsmcobserver.com/tag/activism/" rel="tag">activism</a>, <a href="https://web.archive.org/web/20211016150109/https://ndsmcobserver.com/tag/black-lives-matter/" rel="tag">Black lives matter</a>, <a href="https://web.archive.org/web/20211016150109/https://ndsmcobserver.com/tag/black-owned-businesses/" rel="tag">black-owned businesses</a>, <a href="https://web.archive.org/web/20211016150109/https://ndsmcobserver.com/tag/civil-rights/" rel="tag">Civil Rights</a>, <a href="https://web.archive.org/web/20211016150109/https://ndsmcobserver.com/tag/south-bend/" rel="tag">South Bend</a>, <a href="https://web.archive.org/web/20211016150109/https://ndsmcobserver.com/tag/systemic-racism/" rel="tag">systemic racism</a></p>
</div> 
</article> 
```

From taking a look at the page source, we can see `<div class="content-header">` that marks the article title and `<div class="content-body">` that marks the start of the article text. And we can use a `Control-F`/`Command-F` search to see that the `content-body` class appears only once in the page. This means we can use `.find()` to extract this section of the page.

```Python
# isolate HTML with content-body class
article = soup.find(class_ = "content-body")

# show article HTML
article
```

Now we have the section of HTML with the article text isolated.

```HTML
<p>The Notre Dame Initiative on Race and Resilience hosted a panel Wednesday in DeBartolo Hall on Black civil rights in South Bend, featuring some of South Bend’s prominent community leaders.</p>
<p>The panel, which intended to explore the immense social inequalities facing South Bend’s Black residents, included Trina Robinson, president of NAACP-South Bend; Regina Williams-Preston, president of Community Action for Education and former South Bend Common Council representative; Jorden Giger, co-founder of Black Lives Matter South Bend and Deacon Mel Tardy, deacon of St. Augustine Parish and an advising faculty at the University.</p>
<figure id="attachment_234452" class="wp-caption aligncenter" style="width: 700px"> <div class="media-credit-container aligncenter" style="max-width: 710px">
<img data-attachment-id="234452" data-permalink="https://ndsmcobserver.com/2021/10/south-bend-community-leaders-discuss-role-of-notre-dame-in-fight-for-black-civil-rights/screen-shot-2021-10-15-at-8-36-39-pm/" data-orig-file="https://i1.wp.com/ndsmcobserver.com/wp-content/uploads/2021/10/1634330204-71900895f520822.png?fit=726%2C538&amp;ssl=1" data-orig-size="726,538" data-comments-opened="1" data-image-meta="{&quot;aperture&quot;:&quot;0&quot;,&quot;credit&quot;:&quot;&quot;,&quot;camera&quot;:&quot;&quot;,&quot;caption&quot;:&quot;&quot;,&quot;created_timestamp&quot;:&quot;0&quot;,&quot;copyright&quot;:&quot;&quot;,&quot;focal_length&quot;:&quot;0&quot;,&quot;iso&quot;:&quot;0&quot;,&quot;shutter_speed&quot;:&quot;0&quot;,&quot;title&quot;:&quot;&quot;,&quot;orientation&quot;:&quot;0&quot;}" data-image-title="Screen Shot 2021-10-15 at 8.36.39 PM" data-image-description="" data-medium-file="https://i1.wp.com/ndsmcobserver.com/wp-content/uploads/2021/10/1634330204-71900895f520822.png?fit=700%2C519&amp;ssl=1" data-large-file="https://i1.wp.com/ndsmcobserver.com/wp-content/uploads/2021/10/1634330204-71900895f520822.png?fit=700%2C519&amp;ssl=1" class="wp-image-234452 size-medium" src="https://i1.wp.com/ndsmcobserver.com/wp-content/uploads/2021/10/1634330204-71900895f520822.png?resize=700%2C519&#038;ssl=1" alt="" width="700" height="519" srcset="https://i1.wp.com/ndsmcobserver.com/wp-content/uploads/2021/10/1634330204-71900895f520822.png?resize=700%2C519&amp;ssl=1 700w, https://i1.wp.com/ndsmcobserver.com/wp-content/uploads/2021/10/1634330204-71900895f520822.png?w=726&amp;ssl=1 726w" sizes="(max-width: 700px) 100vw, 700px" data-recalc-dims="1" /><span class="media-credit">Valeria Ortiz | The Observer</span> </div>
<figcaption class="wp-caption-text">In a Wednesday panel, community activists encouraged the University to give to local Black-owned businesses to support inclusion and business growth.</figcaption></figure>
<p>The panelists offered their experiences and recommendations toward a stronger future for civil rights within the local community. They called for action to combat systemic racism — a historical pattern of denying opportunity to fair education, health and housing opportunities in South Bend.</p>
<p>“He who wins the war gets to tell the story, so now we believe it all right. Here we are today seeing how that history gets uncovered,” Williams-Preston said.</p>
```

The next step is to create a list-like object with the sections of text that make up the article. For this web page, those sections are marked by paragraph (`<p>`) tags. We can use `.find_all("p")` to create a list-like object with each `<p>` tag's content as a list item.

```Python
# isolate paragraph tags
paragraphs = article.find_all("p")
```

The last step is to use a `for` loop to iterate over each paragraph in `article_paragraphs`, and use `.contents[]` to extract the paragraph contents and append it to a list. Since the output of `BeautifulSoup`'s `.contents[]` command is still a `BeautifulSoup` object type, we can use the `str()` function to convert the value to a string before appending it to a list.

```Python
# create empty list for paragraphs
paragraph_list = []

# for loop that removes HTML markup for each paragraph or instance of "p" tag
for paragraph in paragraphs:
    paragraph_list.append(str(paragraph.contents[0]))
    
# show list of plain-text paragraphs
paragraph_list
```

Now that we have a working program, we could write each paragraph to a newly-created `.txt` file.

```Python
# create new txt file
f = open("output.txt", "a")

# for loop that removes HTML markup for each paragraph or instance of "p" tag
for paragraph in paragraph_list:
    text = str(paragraph.contents[0])
    f.write(text)
```

We could also combine the `paragraph.contents[0]` `for` loop program with the `for` loop that writes content to a `.txt` file. What that might look like:

```Python
with open("output.txt", "a") as f: # with statement that creates new txt file in append mode
	for paragraph in paragraphs: # for loop that removes HTML markup for each paragraph and writes to txt file
		f.write(str(paragraph.contents[0]))
		f.write("\n") # newline after each paragraph
```

Putting that all together:

```Python
import requests # import requests
from bs4 import BeautifulSoup # import beautifulsoup

page = requests.get("https://web.archive.org/web/20211016150109/https://ndsmcobserver.com/2021/10/south-bend-community-leaders-discuss-role-of-notre-dame-in-fight-for-black-civil-rights/") # get page

soup = BeautifulSoup(page.text, 'html.parser') # create BeautifulSoup object

article = soup.find(class_ = "content-body") # isolate HTML with content-body class

paragraphs = article.find_all("p") # isolate paragraph tags

with open("output.txt", "a") as f: # with statement that creates new txt file in append mode
	for paragraph in paragraphs: # for loop that removes HTML markup for each paragraph and writes to txt file
		f.write(str(paragraph.contents[0]))
		f.write("\n") # newline after each paragraph
```

## Application

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=1b6546d8-c040-4186-b5a5-ade90056af7a">Lab Notebook Questions 12-16</a></td>
  </tr>
  </table>

Q8A: Select another web page that includes unstructured text. From looking at the public web page, what text do you want to scrape from this web page (i.e. specific sections, multiple paragraphs, etc.)?

A few places to start for unstructured text:
- [The Observer!](https://ndsmcobserver.com) (or another news publication of your choosing)
- [WikiSource](https://en.wikisource.org/wiki/Main_Page)(a library of texts that are not covered by copyright)
  * [U.S. Presidential State of the Union Addresses](https://en.wikisource.org/wiki/Portal:State_of_the_Union_Speeches_by_United_States_Presidents)
  * [U.S. Presidential Inaugural Speeches](https://en.wikisource.org/wiki/Portal:Inaugural_Speeches_by_United_States_Presidents)
- [Project Gutenberg](https://www.gutenberg.org) (a library of literary works or texts that are not covered by copyright)

Q8B: Take a look at the HTML for this page. What tags or other HTML components do you see around the section of the page you want to work with? For this question, we're thinking about how we will end up writing a program with `BeautifulSoup` to isolate a section of the web page.

Q8C: Develop an outline for a Python program that scrapes unstructured text from the web page you selected. 

A preliminary workflow:
- Load URL and create BeautifulSoup object
- Isolate section of HTML with your text (either directly or extract from list)
- IF NEEDED: Isolate text elements (create list where each element is a section of text)
- IF NEEDED: Extract text contents (isolate text from each section/paragraph)
- Write text to TXT file

NOTE: You do not need to have working code for all components of this program. That's where we're heading with the final project. At this point, we're focusing on the conceptual framework for the web scraping program. Start to build out code where you can, but think about the programming version of outlining a paper.

Q8D: What challenges or roadblocks did you face working on Q15? What parts of the program do you understand/feel ready to develop at this point? What parts of the program are less clear?

## Oh, the Places You Could Go

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=915f2e6c-5f80-45c3-b44f-ade90058e01f">Oh the Places You Could Go</a></td>
  </tr>
  </table>

Once we have a `.txt` file, we could use Python to generate a list of words used in the article.

```Python
# load file
text = open("output.txt", 'r')

# read file to string
text = text.read()

# create list of words
wordlist = text.split()

# show first 120 words in wordlist
print((wordlist[0:120]))
```

Then, we could use the list of words `wordlist` to count term frequency.

```Python
# create empty list for word frequency
wordfreq = []

# append number of word appearanes to wordfreq list
for word in wordlist:
    wordfreq.append(wordlist.count(word))
    
# create nested list or lists with sublists that include word and number of appearances
str(list(zip(wordlist, wordfreq)))
```

Or, we could connect the terms and frequency count using a dictionary's key-value pairs.

```Python
# convert lists to dictionary using dictionary comprehension
word_count = {wordlist[i]: wordfreq[i] for i in range(len(wordlist))}

# show dictionary
word_count
```

With normalized textual data, we could use Python to do things like:
- count word frequency
  * William J. Turkel and Adam Crymble, "Counting Word Frequencies with Python," The Programming Historian 1 (2012), https://programminghistorian.org/en/lessons/counting-frequencies.
- analyze keywords in contact using n-grams
  * William J. Turkel and Adam Crymble, "Keywords in Context (Using n-grams) with Python," The Programming Historian 1 (2012), https://programminghistorian.org/en/lessons/keywords-in-context-using-n-grams.

Why go to all this  trouble? Computational text analysis or other kinds of natural language processing allow us to see patterns and detect change over time in large bodies of textual materials.

A few projects that do this with speeches given by U.S. presidents:
- [Google News Lab's Inaugurate project](http://inauguratespeeches.com/) that looks at the subjects of inauguration speeches
- ["The Language of the State of the Union,"](https://www.theatlantic.com/politics/archive/2015/01/the-language-of-the-state-of-the-union/384575/) an interactive project from the *Atlantic*'s Ben Schmidt and Mitch Fraas that "reveals how the words presidents use reflect the twists and turns of American history"
- ["Mapping the State of the Union,"](https://www.theatlantic.com/politics/archive/2015/01/mapping-the-state-of-the-union/384576/), also from Schmidt and Fraas, that "shows the 1,410 different spots on the globe presidents have referenced in 224 speeches"

# Why did we do this?

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=32080574-8fa5-4a3b-93a6-ade9005afdca">Why Did We Do This</a></td>
  </tr>
  </table>

At this point, your brain probably hurts. Mine does. Why go to all the trouble of building a Python program when we could just copy and paste the text from an *Observer* article into a `.txt` file, or copy and paste data from Sports Reference into an Excel file or Google Sheet document? Why write a program when we could just remove the markup ourselves through manual data manipulation?

That's a fair question.

Scientific disciplines value research that can be reproduced and replicated. A 2013 editorial in *PLOS Computational Biology* outlines the value of reproducible computational research:
<blockquote>"The importance of replication and reproducibility has recently been exemplified through studies showing that scientific papers commonly leave out experimental details essential for reproduction, studies showing difficulties with replicating published experimental results, an increase in retracted papers, and through a high number of failing clinical trials.
<br>
<br>"We want to emphasize that reproducibility is not only a moral responsibility with respect to the scientific field, but that a lack of reproducibility can also be a burden for you as an individual researcher. As an example, a good practice of reproducibility is necessary in order to allow previously developed methodology to be effectively applied on new data, or to allow reuse of code and results for new projects. In other words, good habits of reproducibility may actually turn out to be a time-saver in the longer run.
<br>
<br>"We further note that reproducibility is just as much about the habits that ensure reproducible research as the technologies that can make these processes efficient and realistic."
<br>
<br>
<em>Sandve GK, Nekrutenko A, Taylor J, Hovig E (2013) Ten Simple Rules for Reproducible Computational Research. PLOS Computational Biology 9(10): e1003285. https://doi.org/10.1371/journal.pcbi.1003285.</em></blockquote>

Manually wrangling or manipulating data makes it difficult for colleagues (and future you) to understand how you got from point A to point B with your data. It also increases the likelihood of human error. In the *PLOS Computational Biology* article, one of the ten rules the authors outline is "Avoid Manual Data Manipulation Steps." The Python workflows we're covering in this lab move in the direction of automating the data scraping/manipulation process, creating a template or workflow others could implement or adapt. 

# Lab Notebook Questions

Lab notebook template:
- [Jupyter Notebook](https://drive.google.com/file/d/1LRsbOC11-8YrPUNBJNAzJDiIM_CQJ3go/view?usp=sharing)


# Final Project Next Steps

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=cc961b6a-ef23-4329-a570-ade9005d8411">Final Project Next Steps</a></td>
  </tr>
  </table>

Our work in this lab is designed to lay the foundation and serve as a springboard for final project work. Specifically, Q4, Q10, and Q13 ask you to develop an outline for web scraping programs using `BeautifulSoup` and `pd.read_html()`. Those questions (and other work for this lab) are the starting place for the final project.

The final project for this course involves a web-scraping project written in Python. Specifically, the final project allows you to select a web page (or web pages) and write a Python program (or programs) that downloads select content from that web page as a plain-text file (`CSV`, `TXT`, etc). That content could be paragraphs of text, tables of data, etc. 

Successful final projects will include two main components:
- a well-documented, working Python program written in Jupyter Notebooks
- a written reflection (minimum 300 words) that documents how you approached the final project/what you wanted to accomplish via the final project, resources consulted, how you handled challenges you encountered, key takeaways, etc.
  * That reflection can come at the end of the Jupyter Notebook or be embedded throughout the Jupyter Notebook, if you want to approach authoring the notebook as a type of tutorial or "report".

Expect to spend at least 10 hours working on the final project. That includes brainstorming, meeting with instructor/TAs, in-class work time, etc. If you’re working on a project that is not going to take that much time, think about how to add complexity or take on another smaller scale project.

Contact the instructor with questions.

So where to start? The instructor and TAs are going to move quickly on getting you feedback on this lab. But your work in Q4, Q10, and Q13 should be the starting place for how you think about and approach the final project. Specifically, think about the kinds of web content you were able to scrape for these questions and how you might further develop, refine, or expand your work.

For example, these questions asked you to develop an outline for specific types of webscraping programs. 
- One next step for the final project could be selecting 1-2 of these programs and further developing or refining the code.
- Another next step (especially if you were able to develop working programs for these questions) is to think about how you could expand or extend these workflows to multiple web pages or other web data sources.
- A third option for next steps would involve thinking expansively about how you could apply the concepts and approaches covered in this lab to a different type of data source/structure. 

So in the interim, as you're waiting for feedback on this lab, think about where you could go next with expanding and extending your work in this lab, and start to flesh out or develop some of your own ideas about where you put your time and effort as you work on the final project.

Contact the instructor with questions.
