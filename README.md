# Data Scraping in Python

<a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license"><img style="border-width: 0;" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" alt="Creative Commons License" /></a>
This tutorial is licensed under a <a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license">Creative Commons Attribution-NonCommercial 4.0 International License</a>.

## Lab Overview

This lab provides an introduction and overview to parsing HTML in Python using the `beautiful soup` package.

[Link to lab overview video](https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=027559db-c0d5-4535-bf95-ace600e36408) (Panopto, ND users).

# Introduction to Beautiful Soup

What is Beautiful Soup? 

"Beautiful Soup is a Python library for pulling data out of HTML and XML files. It works with your favorite parser to provide idiomatic ways of navigating, searching, and modifying the parse tree. It commonly saves programmers hours or days of work" ([Beautiful Soup Documentation](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)

The library name is an allusion to the song Lewis Carroll character the Mock Turtle sings in Chapter 10 of *Alice's Adventures in Wonderland*.

`Beautiful Soup` uses the structure of markup language documents (i.e. HTML, XML, etc) to extract information we can work with in a Python programming environment.

In this lab, we will be focusing on using `Beautiful Soup` to parse and scrape web pages built using HTML and CSS.

# Installing Beautiful Soup

We can install `Beautiful Soup` at the command line using a terminal or shell in our Python environment.

To install `Beautiful Soup` using `pip`:
- `pip install beautifulsoup4`

For more on installing modules using `pip`: Fred Gibbs, "Installing Python Modules with pip," The Programming Historian 2 (2013), https://doi.org/10.46430/phen0029.

We also can install the `lxml` library to help with parsing HTML.

To install `lxml` using `pip`:
- `pip install lxml`

# Loading URLs in Python

We will be using the `requests` library to load URLs in Python.

This library is already built into Python and does not require additional installation.

Core syntax for using the `requests` library to load a URL:

```Python
# import requests
import requests

# load url using get requests.get() method
page = requests.get('URL GOES HERE')
```

# Creating a Beautiful Soup Object

Once we have a URL loaded in Python, we want to be able to use `BeautifulSoup` to parse the web page's HTML components.

We can do that by creating a BeautifulSoup object.

Core syntax:

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

soup = BeautifulSoup(page.text, 'html.parser')
```

Now, we are ready to parse the web page's HTML using `BeautifulSoup`.

# Identifying HTML Tables

HTML uses a few core tags for web pages that include tables.
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

Additional attributes like `align`, `style`, etc. can be used with many of these tags.

# More Adventures in Reading Technical Documentation

Rather than work through a lab procedure that includes step-by-step instructions and guidance designed for students in this class, we're going to get some experience using an online  tutorial written for a general audience.

Tutorial we will be using: Lisa Tagliaferri, "How to Scrape Web Pages With Beautiful Soup and Python 3" *Digital Ocean* (20 March 2019). https://www.digitalocean.com/community/tutorials/how-to-scrape-web-pages-with-beautiful-soup-and-python-3

Open the Digital Ocean ["How to Scrape Web Pages With Beautiful Soup and Python 3"](https://www.digitalocean.com/community/tutorials/how-to-scrape-web-pages-with-beautiful-soup-and-python-3) tutorial in another browser window.

## What is Digital Ocean?

"DigitalOcean, Inc. is an American cloud infrastructure provider headquartered in New York City with data centers worldwide. DigitalOcean provides developers cloud services that help to deploy and scale applications that run simultaneously on multiple computers" ([Wikipedia](https://en.wikipedia.org/wiki/DigitalOcean))

DigitalOcean was founded in 2011 and was part of TechStar's 2012 startup accelerator program.

Initial rounds of funding came from IA Ventures, the Fortress Investment Group, Access Industries, and Andreessen Horowitz.

The company's IPO took place in March 2021.

## Digital Ocean's Education Community

In additional to commercial products and enterprise solutions, DigitalOcean includes robust community forums and staff members dedicated to writing [open educational resources](https://www.digitalocean.com/community/tutorials), like the tutorial we'll be using.

This tutorial was written by [Dr. Lisa Tagliaferri](https://twitter.com/lisaironcutter), who worked as member of the company's Community and Education team before starting as [Sourcegraph's](https://t.co/aQZBLY1hhK?amp=1) Director of Developer Education in February 2021.

The Digital Ocean tutorial walks through scraping data from National Gallery of Art web pages that include artist names and biographical information.

<blockquote>Q1: Include code + comments that document your experience working through the Digital Ocean tutorial.</blockquote>

<blockquote>Q2: Reflect on your experience working through the Digital Ocean tutorial. What challenges did you face? How did you approach or solve them? How was this experience different than previous labs?</blockquote>

Additional tutorials you are welcome to consult as needed:
- Jeri Wieringa, "Intro to Beautiful Soup," *The Programming Historian* 1 (2012), https://doi.org/10.46430/phen0008.
- Martin Breuss, "Beautiful Soup: Build a Web Scraper With Python" *Real Python*. https://realpython.com/beautiful-soup-web-scraper-python/
- DataQuest, "Tutorial: Web Scraping With Python Using Beautiful Soup" *DataQuest* (2 September 2020). https://www.dataquest.io/blog/web-scraping-tutorial-python/

# Additional Lab Notebook Questions

Q3: Select a web page of your choosing and write a Python program that downloads select content from that web page. That content could be files, paragraphs of text, tables od data, etc. Include code + comments.

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

Q1: Include code + comments that document your experience working through the Digital Ocean tutorial.

Q2: Reflect on your experience working through the Digital Ocean tutorial. What challenges did you face? How did you approach or solve them? How was this experience different than previous labs?

Q3: Select a web page of your choosing and write a Python program that downloads select content from that web page. That content could be files, paragraphs of text, tables od data, etc. Include code + comments.

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
