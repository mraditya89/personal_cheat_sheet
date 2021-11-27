### Installation
```
pip install beautifulsoup4
```
### Basic Sintax
```
# import package
from bs4 import BeautifulSoup

# read a html file
with open ('index.html', r) as f:
    doc = BeautifulSoup(f, 'html.parser')

# print doc with style
print(doc.prettify())

# get title tag
titleTag = doc.title

#  find an tag element
tag = doc.find('a') # get the first 'a' html tag

# get text from a tag
text = tag.text

# find multilple tag element
# get all 'p' html tag, wrapped in array
tags = doc.find_all('p') 

# find a text on html
tags = doc.find_all(text='$') 

# get parent result
parentTag = tag.parent

```

### scrape from internet
```
from bs4 import BeautifulSoup
import request

response = request.get(<url>)
    doc = BeautifulSoup(response, 'html.parser')
```
