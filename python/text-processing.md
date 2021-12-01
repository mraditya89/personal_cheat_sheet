## Text Processing In Data Science Projects
[TOC]

## A. Case Folding

### 1. Convert a Text To Lowercase

```gherkin=
text = 'Hello World'
lower_case_text = lowercase(text)
print(lower_case_text)
#hello world
```

### 2. Remove Number
```gherkin=
import re
result = re.sub(r'\d+', '', 'mraditya89')
# mraditya
```
### 3. Remove Punctuation
- Replace Punctiation on a text
```gherkin=
import string

text = "Classic - a book which people praise and don't read!!"
result = text.translate(text.maketrans("","", string.punctuation))
# Classic  a book which people praise and dont read
```

<!-- - Only append a word
```gherkin=
punctuation = string.punctuation
words = ['You','Are','Reading','FinTechExplained', '!', 'NLP', '.']

clean_words = [w for w in words if w not in punctuation]
# ['You','Are','Reading','FinTechExplained', 'NLP']
``` -->

### 4. Remove Whitespaces
```gherkin=
text = "\t Anyone who has never made a mistake has never tried anything new. \n"
result = text.strip() 

# 'Anyone who has never made a mistake has never tried anything new.'
```

## B. Tokenizing
### 1. Tokenise a Paragraph To Sentences

- Use built in python method
```gherkin=
text = "hello world"
token = text.split()
# ["hello", "world"]
```
- Use nltk method
```gherkin=
from nltk.tokenize import word_tokenize

text = "The world as we have created it is a process of our thinking. It cannot be changed without changing our thinking. Albert Einstein"


wordToken = word_tokenize(text)

''' output
[
'The', 'world', 'as', 'we', 'have', 'created', 'it', 'is', 'a', 'process', 'of', 'our', 'thinking.', 
'It', 'can', 'not', 'be', 'changed', 'without', 'changing', 'our', 'thinking.', 
'Albert', 'Einstein'
]
'''
```


### 2. Tokenise a Paragraph To Sentences
```gherkin=
import nltk
from nltk.tokenize import sent_tokenize

text = 'The world as we have created it is a process of our thinking. It cannot be changed without changing our thinking. Albert Einstein'

list = sent_tokenize(text)

''' output
[
'The world as we have created it is a process of our thinking.', 
'It cannot be changed without changing our thinking.'
'Albert Einstein'
]
'''
```



## C. Stopwords

```gherkin=
import nltk
from nltk.corpus import stopwords

text = "There is no friend as loyal as a book"
words = nltk.word_tokenize(text)

stopwords = stopwords.words('english')

# it also works for 'indonesian'

clean = [w for w in words if w not in stopwords]

# ['There', 'friend', 'loyal', 'book']
```

## D. Stemming
### 1. Stemming in English

```gherkin=
from nltk.stem import PorterStemmer
 
st = PorterStemmer()
st.stem('monitoring')
# monitor
```

### 2. Stemming in Bahasa
```gherkin=
from Sastrawi.Stemmer.StemmerFactory import StemmerFactory

factory = StemmerFactory()
stemmer = factory.create_stemmer()

sentence = 'Cara terbaik untuk memprediksi masa depan adalah dengan menciptakannya.'
output   = stemmer.stem(sentence)
print(output)

# cara baik untuk prediksi masa depan adalah dengan cipta

```
