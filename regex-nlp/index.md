# Python RegEx for NLP


## RegEx for NLP

**Natural Language Processing** requires advanced manipulation of the text strings you intend to process. To allow a machine to understand human language it is necessary to divide and group the various elements that compose it; RegEx are the ideal tool to do this. This article, which I will continue to update over time, lists some of the most useful RegEx for NLP, with sample code attached.

## Remove Digits:
How to remove numbers with regex:
```python
import re

# RegEx - Remove digits
pattern = r"\d+"
test_phrase = r"I w4nt 4 sm4rtph0n3. Can you help me? Buy it on https://amazon.com"

result = re.sub(pattern, '', test_phrase)
print(result)
```

## Remove  Symbols
How to remove special characters and symbols with regex:
```python
import re

# RegEx - Remove spechal characters
pattern = r"[^a-zA-Z0-9]+"
test_phrase = r"I want a smartphone. Can you help me? Buy it on https://amazon.com"

result = re.sub(pattern, ' ', test_phrase)
print(result)
```

## Remove Hyperlinks
How to remove Hyperlinks with RegEx:
```python
import re

# RegEx - Remove hyperlinks
pattern = r"http\S+"
test_phrase = r"I want a smartphone. Can you help me? Buy it on https://amazon.com"

result = re.sub(pattern, '', test_phrase)
print(result)
```

## Split Phrases
How to split phrases with RegEx
```python
import re

# RegEx - Split phrases
pattern = r"\.|\!|\?"
test_phrase = r"I want a smartphone. Can you help me? Thanks!"

result = re.split(pattern, test_phrase)
print(result)
```


## Extract prices
How to extract a price with RegEx:
```python
import re

# RegEx - Extract a price
pattern = r"(?:￥|£|€|\$)\s*([\d,]+(?:\.\d+)?)|([\d,]+(?:\.\d+)?)\s*(?:￥|£|€|\$)"
test_phrase = r"I want a smartphone that cost less then €300"

result = re.search(pattern, test_phrase)
print(result.group())
```


## Remove HTML tags
Ho wo remove HTML tags with RegEx
```python
import re

# RegEx - Extract a price
pattern = r"<.*?>"
test_phrase = r"<div>I want a smartphone that cost less then <b>€300</b></div>"

result = re.sub(pattern, '', text)
print(result.group())
```
