# Web Scraping in Python

<a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license"><img style="border-width: 0;" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" alt="Creative Commons License" /></a>
This tutorial is licensed under a <a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license">Creative Commons Attribution-NonCommercial 4.0 International License</a>.

## Lab Overview

This lab provides an introduction and overview to parsing HTML in Python using `beautifulsoup` and `pandas`.

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=a11358d5-c0a6-4bf1-a405-af36017212dc">Lab overview</a></td>
  </tr>
  </table>
  
<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?pid=05f99aec-b0ee-4816-b1e8-af3601753e5b">Lecture/live coding playlist</a></td>
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
- [Beautiful Soup Overview](#beautiful-soup-overview)
- [Beautiful Soup & Structured Data](#beautiful-soup--structured-data)
- [An Alternate Approach: `pandas.read_html()`](#an-alternate-approach-pandasread_html)
- [Beautiful Soup & Unstructured Text](#beautiful-soup--unstructured-text)
  * [Oh, the Places You Could Go](#oh-the-places-you-could-go) 
- [Why did we do this?](#why-did-we-do-this)
- [Lab Notebook Questions](#lab-notebook-questions)
- [Final Project Next Steps](#final-project-next-steps)

[Link to lab procedure as a Jupyter Notebook](https://colab.research.google.com/drive/1Wymv50jxQl3u64qpL8kjDFu4LxUlTiz8?usp=sharing)

# Lecture & Live Coding

Throughout this lab, you will see a Panopto icon at the start of select sections.

This icon indicates there is lecture/live coding asynchronous content that accompanies this section of the lab. 

You can click the link in the figure caption to access these materials (ND users only).

Example:

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=a11358d5-c0a6-4bf1-a405-af36017212dc">Lab overview</a></td>
  </tr>
  </table>
  
<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
<td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?pid=05f99aec-b0ee-4816-b1e8-af3601753e5b">Lecture/live coding playlist</a></td>
  </tr>
  </table>

# Lab Notebook Template

[Click here](https://colab.research.google.com/drive/1-2ahHpMdSzYFSVLnZGfldEoAuyRs5wj7?usp=sharing) to access the lab notebook template as a Jupyter Notebook (Google Colab, ND Users).

# Beautiful Soup Overview

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=7d13378f-8395-40b1-89d0-af3601723136">Getting Started With Beautiful Soup</a></td>
  </tr>
  </table>
  
## Introduction to Beautiful Soup

Table of contents for this section:
- [Introduction to Beautiful Soup](#introduction-to-beautiful-soup)
- [Installing Beautiful Soup](#installing-beautiful-soup)
- [Loading URLs in Python](#loading-urls-in-python)
- [Creating a Beautiful Soup Object](#creating-a-beautiful-soup-object)

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

Table of contents for this section:
- [Concept Refresh](#concept-refresh)
  * [HTML Tables](#html-tables)
  * [File Methods](#file-methods)
- [Using BeautifulSoup with a Single Web Page](#using-beautifulsoup-with-a-single-web-page)
  * [Finding a Table](#finding-a-table)
  * [Extracting the Medal Table](#extract-medal-table)
  * [Testing on a Single Table Row (Single Country)](#testing-on-single-table-row-single-country)
  * [Iterating Over Multiple Rows](#iterating-over-multiple-rows)
- [Application](#application)

## Concept Refresh


<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=a0385ece-2d22-4fd7-84a3-af36017254d6">HTML & File Methods Refresh</a></td>
  </tr>
  </table>

### HTML Tables
 
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

### File I/O

As part of our work in this lab, we'll be saving the content we have scraped from a web page to a plain-text file (either `.txt` or `.csv`), focusing on...
- `open()`
- `write()`

[Click here](https://github.com/kwaldenphd/python-structured-data#file-io--access-modes) to review file I/O and access modes in Python.

## Using BeautifulSoup With a Single Web Page

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=3ee96582-1e15-40e2-b31d-af3601727e35">BeautifulSoup and a Single Web page</a></td>
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

Table of contents for this section:
- [Country Name](#country-name)
- [Country URL](#country-url)
- [Medal Counts](#medal-counts)

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
name = cells[0].contents[0]

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
name = cells[0].contents[0].find('a').contents[0]
```

### Country URL

```HTML
<span id="AFG"><img alt="" class="thumbborder" data-file-height="600" data-file-width="900" decoding="async" height="15" src="//upload.wikimedia.org/wikipedia/commons/thumb/c/cd/Flag_of_Afghanistan_%282013%E2%80%932021%29.svg/22px-Flag_of_Afghanistan_%282013%E2%80%932021%29.svg.png" srcset="//upload.wikimedia.org/wikipedia/commons/thumb/c/cd/Flag_of_Afghanistan_%282013%E2%80%932021%29.svg/33px-Flag_of_Afghanistan_%282013%E2%80%932021%29.svg.png 1.5x, //upload.wikimedia.org/wikipedia/commons/thumb/c/cd/Flag_of_Afghanistan_%282013%E2%80%932021%29.svg/44px-Flag_of_Afghanistan_%282013%E2%80%932021%29.svg.png 2x" width="22"/> <a href="/wiki/Afghanistan_at_the_Olympics" title="Afghanistan at the Olympics">Afghanistan</a> <span style="font-size:90%;">(AFG)</span></span>
```

If we look at the HTML associated with `country_name`, we can see that the country's Wikipedia URL is also in this section of HTML, as part of the `<a href...>` tag. So we can again use `.find()` to isolate the `<a>` tag's contents.

```Python
# get first/only instance of a link tag in HTML for single country
link = cells[0].find('a')

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
link = cells[0].find('a').get('href')
link = "https://en.wikipedia.org" + link
print(link)
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
combined_olympics = cells[11].contents[0].strip()

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
medals.insert(0, name)
medals.insert(1, link)

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

Now we're ready to iterate over each country (table row) using the code we tested on a single country. We can create a list with each row's values and append that list as a sublist or nested list to an empty list.

```Python
table_rows = [] # empty list for data

for row in rows: # for loop that iterates over rows
  tags = [] # create empty list for td tags in single row
	
  cells = row.find_all('td') # isolate cells, td elements
	
  tags.append(cells) # append tags to tag list
	
  for cells in tags:
    try:
      name = cells[0].contents[0].find('a').contents[0] # combined program for country name
      link = cells[0].find('a').get('href') # for loop that iterates over cells in row
      link = "https://en.wikipedia.org" + link
      summer = cells[1].contents[0] # number of summer olympic appearances
      summer_gold = cells[2].contents[0] # number of summer gold medals
      summer_silver = cells[3].contents[0] # number of summer silver medals
      summer_bronze = cells[4].contents[0] # number of summer bronze medals
      summer_medals = cells[5].contents[0].strip() # total number of summer olympics medals, using strip() to remove line break
      winter = cells[6].contents[0] # total number of winter olympic appearances
      winter_gold = cells[7].contents[0] # number of winter gold medals
      winter_silver = cells[8].contents[0] # number of winter silver
      winter_bronze = cells[9].contents[0] # number of winter bronze
      winter_medals = cells[10].contents[0].strip() # total number of winter medals
      combined_olympics = cells[11].contents[0].strip() # total number combined olympic appearances
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
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=b7e2f787-47cf-4f61-af59-af3601729e4d">Lab Notebook Questions 1-2</a></td>
  </tr>
  </table>

Q1A: Select another Wikipedia page that includes a table. From looking at the public web page, what data do you want to scrape from this web page (i.e. specific table, multiple tables, etc.)? What do you want the resulting data structure to look like (columns, rows, etc)?

Q1B: Take a look at the HTML for this page. What tags or other HTML components do you see around the section of the page you want to work with? For this question, we're thinking about how we will end up writing a program with <code>BeautifulSoup</code> to isolate a section of the web page.

Q1C: Develop an outline for a Python program that scrapes data from the web page you selected. 

A preliminary workflow:
- Load URL and create BeautifulSoup object
- Isolate section of HTML with your table (either directly or extract from list)
- Isolate table row elements (create list where each element is a table row)
- Extract contents from row (isolate the pieces of information from each row)
- Create Pandas DataFrame
- Write extracted row contents to CSV file

NOTE: This program will have a lot of moving parts! Starting with pseudocode to think about the underlying logic can help you organize the components you're building. As you start to build out your own program, think about where you can draw on sample code from the lab (or follow the same conceptual workflow).

Q1D: What challenges or roadblocks did you face working on Q1C? How did you start to tackle or solve them? 

# An Alternate Approach: pandas.read_html()

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=f02d35d9-bb7f-4503-9f79-af360172f44e">pandas.read_html()</a></td>
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
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=234b8c5b-7641-47bf-a61c-af3601731318">Lab Notebook Questions 5-7</a></td>
  </tr>
  </table>
  
Q2A: Develop an outline for a Python program that uses `pd.read_html()` to scrape data from a web page of your choosing.
- *Wikipedia tables are fair game, but folks interested in sport data may want to head over to a [Sports Reference](https://www.sports-reference.com/) site.*

A preliminary workflow:
- Use `pd.read_html()` to create a list of DataFrame objects
- Identify which DataFrame object in the list is the table you want to work with
- Isolate the list element to create a new DataFrame
- Write the new DataFrame to a CSV file

NOTE: Even though `pd.read_html()` has an easier learning curve than `BeautifulSoup`, this program will have a few moving parts! Starting with pseudocode to think about the underlying logic can help you organize the components you're building. As you start to build out your own program, think about where you can draw on sample code from the lab (or follow the same conceptual workflow).

ANOTHER NOTE: For many Sports Reference pages, tables further down the page are buried in HTML comments. These tables will not show up when you use `pd.read_html()`. We can come back to these "hidden tables" in the final project, but for now, focus on the tables that do show up when you use `pd.read_html()`.

Q3B: What challenges or roadblocks did you face working on Q3A? How did you start to tackle or solve them? 

# `Beautiful Soup` & Unstructured Text

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=13f5e27a-d21f-48a8-883b-af360173332a">Unstructured Text</a></td>
  </tr>
  </table>

So far, this lab has focused on approaches for scraping structured data from the web using Python. But there are other contexts and use cases when we might want to be able to scrape unstructured text from the web and be able to work with that "data" in Python (or write it to a plain-text `.txt` file). 

For example, take a look at U.S. President John F. Kennedy's 1961 inaugural address: https://en.wikisource.org/wiki/John_F._Kennedy%27s_Inaugural_Address

Imagine we wanted to use Python to analyze the words or terms used in this text. The first step would be to get a plain-text `.txt` version of the article text.  We would start with the same `BeautifulSoup` workflow we've used previously:
- Load URL
- Create `BeautifulSoup` object
- Isolate section of HTML with speech text

```Python
# get page
page = requests.get("https://en.wikisource.org/wiki/John_F._Kennedy%27s_Inaugural_Address")

# create BeautifulSoup object
soup = BeautifulSoup(page.text, 'html.parser')

# show BeautifulSoup object
soup
```

Next, we want to isolate the section of the page that includes the article text.

```HTML
<span class="&#95;_watch ws-noexport noprint"><figure class="mw-default-size mw-halign-right" typeof="mw:File/Thumb"><span><video id="mwe_player_1" poster="//upload.wikimedia.org/wikipedia/commons/thumb/7/74/John_F._Kennedy_Inauguration_Speech.ogv/220px--John_F._Kennedy_Inauguration_Speech.ogv.jpg" controls="" preload="none" class="mw-file-element" width="220" height="165" data-durationhint="931" data-mwtitle="John_F._Kennedy_Inauguration_Speech.ogv" data-mwprovider="wikimediacommons" resource="/wiki/File:John_F._Kennedy_Inauguration_Speech.ogv"><source src="//upload.wikimedia.org/wikipedia/commons/transcoded/7/74/John_F._Kennedy_Inauguration_Speech.ogv/John_F._Kennedy_Inauguration_Speech.ogv.480p.vp9.webm" type="video/webm; codecs=&quot;vp9, opus&quot;" data-transcodekey="480p.vp9.webm" data-width="640" data-height="480" /><source src="//upload.wikimedia.org/wikipedia/commons/7/74/John_F._Kennedy_Inauguration_Speech.ogv" type="video/ogg; codecs=&quot;theora, vorbis&quot;" data-width="640" data-height="480" /><source src="//upload.wikimedia.org/wikipedia/commons/transcoded/7/74/John_F._Kennedy_Inauguration_Speech.ogv/John_F._Kennedy_Inauguration_Speech.ogv.240p.vp9.webm" type="video/webm; codecs=&quot;vp9, opus&quot;" data-transcodekey="240p.vp9.webm" data-width="320" data-height="240" /><source src="//upload.wikimedia.org/wikipedia/commons/transcoded/7/74/John_F._Kennedy_Inauguration_Speech.ogv/John_F._Kennedy_Inauguration_Speech.ogv.360p.vp9.webm" type="video/webm; codecs=&quot;vp9, opus&quot;" data-transcodekey="360p.vp9.webm" data-width="480" data-height="360" /><source src="//upload.wikimedia.org/wikipedia/commons/transcoded/7/74/John_F._Kennedy_Inauguration_Speech.ogv/John_F._Kennedy_Inauguration_Speech.ogv.360p.webm" type="video/webm; codecs=&quot;vp8, vorbis&quot;" data-transcodekey="360p.webm" data-width="480" data-height="360" /><track src="https://commons.wikimedia.org/w/api.php?action=timedtext&amp;title=File%3AJohn_F._Kennedy_Inauguration_Speech.ogv&amp;lang=en&amp;trackformat=vtt&amp;origin=%2A" kind="subtitles" type="text/vtt" srclang="en" label="English ‪(en)‬" data-dir="ltr" /></video></span><figcaption>John F. Kennedy delivering his inaugural address<br />(<small>241.44 MB,&#32;15m 30s,&#32;<a href="https://commons.wikimedia.org/wiki/Project:Media_help" class="extiw" title="commons:Project:Media help">help</a>,&#32;<a href="https://commons.wikimedia.org/wiki/File:John_F._Kennedy_Inauguration_Speech.ogv" class="extiw" title="commons:File:John F. Kennedy Inauguration Speech.ogv">file info or download</a></small>)</figcaption></figure></span>
<p>Vice President Johnson, Mr. Speaker, Mr. Chief Justice, President Eisenhower, Vice President Nixon, President Truman, Reverend Clergy, fellow citizens:
</p><p>We observe today not a victory of party but a celebration of freedom, symbolizing an end as well as a beginning, signifying renewal as well as change. For I have sworn before you and Almighty God the same solemn oath our forbears prescribed nearly a century and three-quarters ago.
</p><p>The world is very different now. For man holds in his mortal hands the power to abolish all forms of human poverty and all forms of human life. And yet the same revolutionary beliefs for which our forebears fought are still at issue around the globe–the belief that the rights of man come not from the generosity of the state but from the hand of God.
</p><p>We dare not forget today that we are the heirs of that first revolution. Let the word go forth from this time and place, to friend and foe alike, that the torch has been passed to a new generation of Americans, born in this century, tempered by war, disciplined by a hard and bitter peace, proud of our ancient heritage, and unwilling to witness or permit the slow undoing of those human rights to which this nation has always been committed, and to which we are committed today at home and around the world.
</p><p>Let every nation know, whether it wishes us well or ill, that we shall pay any price, bear any burden, meet any hardship, support any friend, oppose any foe to assure the survival and the success of liberty.
</p><p>This much we pledge–and more.
</p><p>To those old allies whose cultural and spiritual origins we share, we pledge the loyalty of faithful friends. United there is little we cannot do in a host of cooperative ventures. Divided there is little we can do; for we dare not meet a powerful challenge at odds and split asunder.
</p><p>To those new states whom we welcome to the ranks of the free, we pledge our word that one form of colonial control shall not have passed away merely to be replaced by a far more iron tyranny. We shall not always expect to find them supporting our view. But we shall always hope to find them strongly supporting their own freedom; and to remember that, in the past, those who foolishly sought power by riding the back of the tiger ended up inside.
</p><p>To those people in the huts and villages of half the globe struggling to break the bonds of mass misery, we pledge our best efforts to help them help themselves, for whatever period is required–not because the communists may be doing it, not because we seek their votes, but because it is right. If a free society cannot help the many who are poor, it cannot save the few who are rich.
</p><p>To our sister republics south of our border, we offer a special pledge: to convert our good words into good deeds in a new alliance for progress; to assist free men and free governments in casting off the chains of poverty. But this peaceful revolution of hope cannot become the prey of hostile powers. Let all our neighbors know that we shall join with them to oppose aggression or subversion anywhere in the Americas. And let every other power know that this Hemisphere intends to remain the master of its own house.
</p><p>To that world assembly of sovereign states, the United Nations, our last best hope in an age where the instruments of war have far outpaced the instruments of peace, we renew our pledge of support, to prevent it from becoming merely a forum for invective, to strengthen its shield of the new and the weak, and to enlarge the area in which its writ may run.
</p><p>Finally, to those nations who would make themselves our adversary, we offer not a pledge but a request: that both sides begin anew the quest for peace, before the dark powers of destruction unleashed by science engulf all humanity in planned or accidental self-destruction.
</p><p>We dare not tempt them with weakness. For only when our arms are sufficient beyond doubt can we be certain beyond doubt that they will never be employed.
</p><p>But neither can two great and powerful groups of nations take comfort from our present course–both sides overburdened by the cost of modern weapons, both rightly alarmed by the steady spread of the deadly atom, yet both racing to alter that uncertain balance of terror that stays the hand of mankind's final war.
</p><p>So let us begin anew–remembering on both sides that civility is not a sign of weakness, and sincerity is always subject to proof. Let us never negotiate out of fear. But let us never fear to negotiate.
</p><p>Let both sides explore what problems unite us instead of belaboring those problems which divide us.
</p><p>Let both sides, for the first time, formulate serious and precise proposals for the inspection and control of arms–and bring the absolute power to destroy other nations under the absolute control of all nations.
</p><p>Let both sides seek to invoke the wonders of science instead of its terrors. Together let us explore the stars, conquer the deserts, eradicate disease, tap the ocean depths and encourage the arts and commerce.
</p><p>Let both sides unite to heed in all corners of the Earth the command of Isaiah to "<a href="/wiki/Bible_(King_James)/Isaiah#Chapter_58" title="Bible (King James)/Isaiah">undo the heavy burdens ... (and) let the oppressed go free.</a>"
</p><p>And if a beachhead of cooperation may push back the jungle of suspicion, let both sides join in creating a new endeavor, not a new balance of power, but a new world of law, where the strong are just and the weak secure and the peace preserved.
</p><p>All this will not be finished in the first one hundred days. Nor will it be finished in the first one thousand days, nor in the life of this Administration, nor even perhaps in our lifetime on this planet. But let us begin.
</p><p>In your hands, my fellow citizens, more than mine, will rest the final success or failure of our course. Since this country was founded, each generation of Americans has been summoned to give testimony to its national loyalty. The graves of young Americans who answered the call to service surround the globe.
</p><p>Now the trumpet summons us again; not as a call to bear arms, though arms we need; not as a call to battle, though embattled we are; but a call to bear the burden of a long twilight struggle, year in and year out, "<a href="/wiki/Bible_(King_James)/Romans#Chapter_12" title="Bible (King James)/Romans">rejoicing in hope, patient in tribulation</a>"–a struggle against the common enemies of man: tyranny, poverty, disease and war itself.
</p><p>Can we forge against these enemies a grand and global alliance, North and South, East and West, that can assure a more fruitful life for all mankind? Will you join in that historic effort?
</p><p>In the long history of the world, only a few generations have been granted the role of defending freedom in its hour of maximum danger. I do not shrink from this responsibility; I welcome it. I do not believe that any of us would exchange places with any other people or any other generation. The energy, the faith, the devotion which we bring to this endeavor will light our country and all who serve it–and the glow from that fire can truly light the world.
</p><p>And so, my fellow Americans: ask not what your country can do for you–ask what you can do for your country.
</p><p>My fellow citizens of the world: ask not what America will do for you, but what together we can do for the freedom of man.
</p><p>Finally, whether you are citizens of America or citizens of the world, ask of us here the same high standards of strength and sacrifice which we ask of you. With a good conscience our only sure reward, with history the final judge of our deeds, let us go forth to lead the land we love, asking His blessing and His help, but knowing that here on Earth God's work must truly be our own.
</p><p><br />
</p>
```

From taking a look at the page source, we can see `<p>` (paragraph tags) mark each paragraph. And we can use a `Control-F`/`Command-F` search to see that that most of the `<p>` tags appear around the text of the speech. 

We can use `.find_all("p")` to create a list-like object with each `<p>` tag's content as a list item.

```Python
# isolate paragraph tags
paragraphs = soup.find_all("p")

# show number of paragraphs
len(paragraphs)
```

```Python
# show first paragraph
paragraphs[0]
```

```Python
# show last paragraph
paragraphs[-1]
```

We'll need to subset the `paragraphs` list to get just the `<p>` tags that have the speech text. We can do this using list indexing.

```Python
subset = paragraphs[1:29] # subset paragraph tags
subset[0].contents[0].strip() # isolate single paragraph; strip removes the "\n" new line regular expression
```

So now we have just the `<p>` tags connected to the speech. The last step is to use a `for` loop to iterate over each paragraph in `article_paragraphs`, and use `.contents[]` to extract the paragraph contents and append it to a list. Since the output of `BeautifulSoup`'s `.contents[]` command is still a `BeautifulSoup` object type, we can use the `str()` function to convert the value to a string before appending it to a list.

```Python
for p in subset: # iterate over paragraphs
  print(p.contents[0].strip()) # show text
```

```Python
lines = [] # empty list for text

for p in subset: # iterate over paragraphs
  lines.append(str(p.contents[0].strip())) # isolate p tag contents and append to list

lines[0] # show first line
```

Now that we have a working program, we could write each paragraph to a newly-created `.txt` file.

```Python
with open("output.txt", "a") as f: # new file
  for p in subset: # iterate over paragraphs
    f.write(str(p.contents[0].strip())) # write paragraph to file
    f.write("\n") # preserve line breaks
```

Putting that all together:

```Python
# import statements
import requests, csv, pandas as pd
from bs4 import BeautifulSoup

# load page
page = requests.get("https://en.wikisource.org/wiki/John_F._Kennedy%27s_Inaugural_Address")

# beautifulsoup object
soup = BeautifulSoup(page.text, 'html.parser')

# isolate paragraph tags
paragraphs = soup.find_all('p')

# subset paragraph tags
subset = paragraphs[1:29]

# write output to text file
with open("output.txt", "a") as f: # new file
  for p in subset: # iterate over paragraphs
    f.write(str(p.contents[0].strip())) # write paragraph to file
    f.write("\n") # preserve line breaks
    print(p.contents[0].strip()) # show paragraph
```

## Application

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=ee5be045-9655-4f34-a03e-af36017356f3">Lab Notebook Question 8</a></td>
  </tr>
  </table>

Q4A: Select another web page that includes unstructured text. From looking at the public web page, what text do you want to scrape from this web page (i.e. specific sections, multiple paragraphs, etc.)?

A few places to start for unstructured text:
- [WikiSource](https://en.wikisource.org/wiki/Main_Page)(a library of texts that are not covered by copyright)
  * [U.S. Presidential State of the Union Addresses](https://en.wikisource.org/wiki/Portal:State_of_the_Union_Speeches_by_United_States_Presidents)
  * [U.S. Presidential Inaugural Speeches](https://en.wikisource.org/wiki/Portal:Inaugural_Speeches_by_United_States_Presidents)
- [Project Gutenberg](https://www.gutenberg.org) (a library of literary works or texts that are not covered by copyright)

Q4B: Take a look at the HTML for this page. What tags or other HTML components do you see around the section of the page you want to work with? For this question, we're thinking about how we will end up writing a program with `BeautifulSoup` to isolate a section of the web page.

Q4C: Develop an outline for a Python program that scrapes unstructured text from the web page you selected. 

A preliminary workflow:
- Load URL and create BeautifulSoup object
- Isolate section of HTML with your text (either directly or extract from list)
- IF NEEDED: Isolate text elements (create list where each element is a section of text)
- IF NEEDED: Extract text contents (isolate text from each section/paragraph)
- Write text to TXT file

NOTE: This program will have a lot of moving parts! Starting with pseudocode to think about the underlying logic can help you organize the components you're building. As you start to build out your own program, think about where you can draw on sample code from the lab (or follow the same conceptual workflow).

Q4D: What challenges or roadblocks did you face working on Q4C? How did you start to tackle or solve them? 

## Oh, the Places You Could Go

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=b27a90ce-1247-4f24-bf63-af3601737891">Oh the Places You Could Go</a></td>
  </tr>
  </table>

Once we have the isolated text, we could use Python to generate a list of words used in the speech.

```Python
lines = [] # empty list for text

for p in subset: # iterate over paragraphs
  lines.append(str(p.contents[0].strip())) # isolate p tag contents and append to list

lines[0] # show first line
```

```Python
speech = "\n".join(lines) # use list method to concatenate list items
print(speech) # show speech text
```

```Python
wordlist = speech.split() # list of words
print((wordlist[0:120])) # show first 120 words in wordlist
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

We could also put that data in a Pandas DataFrame.

```Python
# import pandas
import pandas as pd

# create dataframe
df = pd.DataFrame(list(word_count.items()), columns=['term', 'count'])

# show df with count column sorted
df.sort_values('count')
```

And once it's in a DataFrame, we could filter or subset the data, by...

Filtering out commonly-used words:

```Python
# stopwords
stopWords = ['a', 'an', 'and', 'the', 'has', 'to', 'of', 'that', 'in', 'for', 'this']

# filter out rows that match list value
subset = df[~df['term'].isin(stopWords)]

# show updated df
subset.sort_values('count')
```

Filtering out rows with terms that only appear 1-2 times.

```Python
# filter out terms that only 1-2 times
subset = subset[subset['count'] > 2]

# show updated df
subset.sort_values('count')
```

With normalized textual data, we could use Python to do things like:
- count word frequency
  * William J. Turkel and Adam Crymble, "Counting Word Frequencies with Python," The Programming Historian 1 (2012), https://programminghistorian.org/en/lessons/counting-frequencies.
- analyze keywords in contact using n-grams
  * William J. Turkel and Adam Crymble, "Keywords in Context (Using n-grams) with Python," The Programming Historian 1 (2012), https://programminghistorian.org/en/lessons/keywords-in-context-using-n-grams.

Why go to all this  trouble? Computational text analysis or other kinds of natural language processing allow us to see patterns and detect change over time in large bodies of textual materials.

A few projects that do this with speeches given by U.S. presidents:
- [Google News Lab's Inaugurate project](http://inauguratespeeches.com/) that looks at the subjects of inauguration speeches
- ["The Language of the State of the Union,"](https://web.archive.org/web/20160115062935/https://www.theatlantic.com/politics/archive/2015/01/the-language-of-the-state-of-the-union/384575/) an interactive project from the *Atlantic*'s Ben Schmidt and Mitch Fraas that "reveals how the words presidents use reflect the twists and turns of American history"
- ["Mapping the State of the Union,"](https://web.archive.org/web/20160111132255/https://www.theatlantic.com/politics/archive/2015/01/mapping-the-state-of-the-union/384576/), also from Schmidt and Fraas, that "shows the 1,410 different spots on the globe presidents have referenced in 224 speeches"

# Why did we do this?

<table>
 <tr><td>
<img src="https://elearn.southampton.ac.uk/wp-content/blogs.dir/sites/64/2021/04/PanPan.png" alt="Panopto logo" width="50"/></td>
  <td><a href="https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=30d2c0df-f48c-466a-bfa8-af3601739408">Why Did We Do This</a></td>
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

[Click here](https://colab.research.google.com/drive/1-2ahHpMdSzYFSVLnZGfldEoAuyRs5wj7?usp=sharing) to access the lab notebook template as a Jupyter Notebook (Google Colab, ND Users).

Q1A: Select another Wikipedia page that includes a table. From looking at the public web page, what data do you want to scrape from this web page (i.e. specific table, multiple tables, etc.)? What do you want the resulting data structure to look like (columns, rows, etc)?

Q1B: Take a look at the HTML for this page. What tags or other HTML components do you see around the section of the page you want to work with? For this question, we're thinking about how we will end up writing a program with <code>BeautifulSoup</code> to isolate a section of the web page.

Q1C: Develop an outline for a Python program that scrapes data from the web page you selected. 

A preliminary workflow:
- Load URL and create BeautifulSoup object
- Isolate section of HTML with your table (either directly or extract from list)
- Isolate table row elements (create list where each element is a table row)
- Extract contents from row (isolate the pieces of information from each row)
- Create Pandas DataFrame
- Write extracted row contents to CSV file

NOTE: You do not need to have working code for all components of this program. That's where we're heading with the final project. At this point, we're focusing on the conceptual framework for the web scraping program. Start to build out code where you can, but think about the programming version of outlining a paper.

Q2D: What challenges or roadblocks did you face working on Q2C? What parts of the program do you understand/feel ready to develop at this point? What parts of the program are less clear?

Q7A: Develop an outline for a Python program that uses `pd.read_html()` to scrape data from one of the web pages you select in Q6.

A preliminary workflow:
- Use `pd.read_html()` to create a list of DataFrame objects
- Identify which DataFrame object in the list is the table you want to work with
- Isolate the list element to create a new DataFrame
- Write the new DataFrame to a CSV file

NOTE: For Q3, you did not need to have working code for all components of this program. Since `pd.read_html()` has an easier learning curve, let's see if we can flesh out more of this program. But if you run into problems, it's okay to focus on the conceptual framework for the web scraping program. Start to build out code where you can, but think about the programming version of outlining a paper.

ANOTHER NOTE: For many Sports Reference pages, tables further down the page are buried in HTML comments. These tables will not show up when you use `pd.read_html()`. We can come back to these "hidden tables" in the final project, but for now, focus on the tables that do show up when you use `pd.read_html()`.

Q7B: What challenges or roadblocks did you face working on Q7A? What parts of the program do you understand and/or were able to develop? What parts of the program are less clear?

Q8A: Select another web page that includes unstructured text. From looking at the public web page, what text do you want to scrape from this web page (i.e. specific sections, multiple paragraphs, etc.)?

A few places to start for unstructured text:
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

Q8D: What challenges or roadblocks did you face working on Q8C? What parts of the program do you understand/feel ready to develop at this point? What parts of the program are less clear?
