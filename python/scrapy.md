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
text = tag.string

# find multilple tag element
# get all 'p' html tag, wrapped in array
tags = doc.find_all('p') 

# find a text on html
tags = doc.find_all(text='$') 

# find tag with specific classname
tags = doc.find_all("div", class_='quote')

# Available parameter on tag filter: class_, value, name, id, limit

# get parent result
parentTag = tag.parent

# get children result
childrenTag = tag.children

# get a sibling
nextSiblingTag = tag.next_sibling
prevSiblingTag = tag.previous_sibling

# get siblings
# return list of tags
nextSiblingTags = tag.next_siblings
```

### scrape from internet
```
from urllib.request import Request, urlopen

from bs4 import BeautifulSoup

url = 'http://quotes.toscrape.com/'
request = Request(url)
response = urlopen(request)

doc = BeautifulSoup(response, 'html.parser')
print(doc.prettify())

```

### manipulate 
```
from bs4 import BeautifulSoup

# open a index.html file
with open('index.html', 'r') as f:
  doc = BeautifulSoup(f, 'html.parser')

# find input tags
tags = doc.find_all('input', text='text')

# manipulate placeholder
for tag in tags:
  tag['placeholder'] = 'I changed you'

# write a file
with open('modified_index.html', 'w') as file:
  file.write(str(doc))
```
