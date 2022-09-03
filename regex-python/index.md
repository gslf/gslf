# RegEx in python


## What is a RegEx
A RegEx (Regular Expression) is a powerfull tool for search and extract patterns in text, and is fundamental for NLP (Natural Language Processing). The scope of this tool is very broad, ranging from web scraping to Big Data analysis systems. The standard Python library integrates the **re** module which contains everything needed to use RegEx.

## RegEx functions
To use a RegEx in python just import the ** re ** module and use one of the functions available to search for patterns.

| Function | Use                                              
|----------|-----------
|search    | Scan through string looking for the first location where the regular expression pattern produces a match, and return a corresponding match object
|findall   | Return all non-overlapping matches of pattern in string, as a list of strings or tuples.
|finditer  | Return an iterator yielding match objects over all non-overlapping matches for the RE pattern in string.
|split     | Split string by the occurrences of pattern.
|sub       | Return the string obtained by replacing the leftmost non-overlapping occurrences of pattern in string by the replacement repl.

```python
import re

sample_txt = "Hello World, hello world!"
sample_pattern = "hello"

search_result = re.search(sample_pattern, sample_txt)
print("Search result:")
print(search_result)
#Search result:
#re.Match object; span=(13, 18), match='hello'>

findall_result = re.findall(sample_pattern, sample_txt)
print("Findall result:")
print(findall_result)
#Findall result:
#['hello']

finditer_result = re.finditer(sample_pattern, sample_txt)
print("Finditer result:")
print(finditer_result)
#Finditer result:
#<callable_iterator object at 0x102ad3700>

split_result = re.split(sample_pattern, sample_txt)
print("Split result:")
print(split_result)
#Split result:
#['Hello World, ', ' world!']

sub_result = re.sub(sample_pattern, "goodmorning",  sample_txt)
print("Sub result:")
print(sub_result)
#Sub result:
#Hello World, goodmorning world!

```

## RegEx basic pattern rules
The functions are very simple to use, but you have to define a pattern, and this is slightly more complex. Patterns are defined as strings that contain certain character sequences that define the rules used to match against a string. In the table below there are the most used rules in RegEx, just below some examples that show how to use them in practice.

| Rule     | Use                                              
|----------|-----------
|[]| A set of characters to match
|{}| Number of occurences
|()| Group
|$| End with
|^| Start with
|*| Zero or more occurrences
|+| One or more occurrences
|?| Zero or one occurrences

```python
import re

# Find all numbers
txt= "test1234regex"
pattern = r"[0-9]"
result = re.findall(pattern, txt)
print(result) # ['1', '2', '3', '4']

# Find all number couples
txt= "test1234regex"
pattern = r"[0-9]{2}"
result = re.findall(pattern, txt)
print(result) # ['12', '34']

# Find a word that start with t and end with t
txt= "test"
pattern = r"^t\w+t$"
result = re.findall(pattern, txt)
print(result) # ['test']

# Find all numbers
txt= "The quick brown fox jumps over the lazy dog."
pattern = r"\b\w{5}\b"
result = re.findall(pattern, txt)
print(result) # ['quick', 'brown', 'jumps']
```



