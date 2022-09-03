# [NLP] How to clean and tokenize text in python


## Prepare text for NLP
**Natural Language Processing** allows machines to interpret text, but to perform this task in the best possible way it is necessary to sort and clean the text, so as to make it "understandable" to the algorithm. For simplicity we divide this complex task into two simpler ones, first we will take care of cleaning the text and then dividing it into tokens.

## Step 1: Clean text
Often the text to be processed comes from the web, so the first thing to do is remove all the HTML tags. We can do this with a regex.
```python
import re

# Remove HTML Tags
pattern = r"<.*?>"
plain_text = re.sub(pattern, '', text)
```
After that we need to decode all HTML entities, such as & nbsp; (representing an empty space), or & amp; (representing an ampersand).
```python
from html import unescape

# Decode HTML entities
decoded_text = unescape(plain_text)
```

Now we can remove all the multiple spaces and make all the text lowercase.
```python
# Remove multiple spaces
pattern = r"\s\s+"
unspaced_text = re.sub(pattern, " ", decoded_text)

# Case conversion
lowered_text = unspaced_text.lower()
```

At the and we can remove all accentend and exotic characters.
```
import unicodedata

# Remove accented characters
clean_text = unicodedata.normalize('NFKD', lowered_text).encode('ascii', 'ignore').decode('utf-8', 'ignore')
```


Now we are ready for tokenization.

## Step 3: Tokenize text
Two different levels of tokenization are required for the subsequent text processing steps, which allow NLP algorithms to extract information and interpretation. In the first level we divide the sentences present in the text. In the next level we divide the sentences into single words.

```python
import nltk

# Sentence Tokenization
sentences = nltk.sent_tokenize(text)

for sentence in sentences:
    words = nltk.word_tokenize(sentence)
    result.append(words)
```

## The Full Code
```python
import re
import unicodedata
import nltk
from html import unescape

def textCleaner(text):
    # Remove HTML Tags
    pattern = r"<.*?>"
    plain_text = re.sub(pattern, '', text)

    # Decode HTML entities
    decoded_text = unescape(plain_text)

    # Remove multiple spaces
    pattern = r"\s\s+"
    unspaced_text = re.sub(pattern, " ", decoded_text)

    # Case conversion
    lowered_text = unspaced_text.lower()

    # Remove accented characters
    clean_text = unicodedata.normalize('NFKD', lowered_text).encode('ascii', 'ignore').decode('utf-8', 'ignore')

    
    return clean_text

def tokenization(text):
    result = []
    
    # Sentence Tokenization
    sentences = nltk.sent_tokenize(text)

    for sentence in sentences:
        words = nltk.word_tokenize(sentence)
        result.append(words)

    
    return result
```

## Sample Output
Let's test this code, with a sample html text from the first web page ever.

```python
sample_html = "<HEADER> <TITLE>The World Wide Web project</TITLE> </HEADER> \
                    <BODY><H1>World Wide Web</H1> Thhe WorldWideWeb (W3) is a wide-area<A NAME=0 HREF=\"WhatIs.html\"> hypermedia</A> information retrieval \
                    initiative aiming to give universal access to a large universe of documents.<P> Everything there is onlinè about W3 is linked \
                    directly or indirectly to this documnet, including an <A NAME=24 HREF=\"Summary.html\">executive summary</A> of the project, <A\
                    NAME=29 HREF=\"Administration/Mailling/Overview.html\">Mailing lists</A>, <ANAME=30 HREF=\"Policy.html\">Policy</A> , November's  <A \
                    NAME=34 HREF=\"News/9211.html\">W3  news</A> ,<A NAME=41 HREF=\"FAQ/List.html\">Frequently Asked Questions</A> &nbsp;.</BODY>'"

clean_text = textCleaner(sample_html)
print(clean_text)

tokenized_text = tokenization(clean_text)
print(tokenized_text)
```

The output:
```
the world wide web project world wide web thhe worldwideweb (w3) is a wide-area hypermedia information retrieval initiative aiming to give universal access to a large universe of documents. everything there is online about w3 is linked directly or indirectly to this documnet, including an executive summary of the project, mailing lists, policy , november's w3 news ,frequently asked questions .'

[['the', 'world', 'wide', 'web', 'project', 'world', 'wide', 'web', 'thhe', 'worldwideweb', '(', 'w3', ')', 'is', 'a', 'wide-area', 'hypermedia', 'information', 'retrieval', 'initiative', 'aiming', 'to', 'give', 'universal', 'access', 'to', 'a', 'large', 'universe', 'of', 'documents', '.'], ['everything', 'there', 'is', 'online', 'about', 'w3', 'is', 'linked', 'directly', 'or', 'indirectly', 'to', 'this', 'documnet', ',', 'including', 'an', 'executive', 'summary', 'of', 'the', 'project', ',', 'mailing', 'lists', ',', 'policy', ',', 'november', "'s", 'w3', 'news', ',', 'frequently', 'asked', 'questions', '.', "'"]]
```
