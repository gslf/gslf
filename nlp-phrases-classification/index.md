# [NLP] Phrases Classification


## Intro
Proper ordering and proper classification of sentences is critical to enabling machines to interpret human language. The **phrases classification** is therefore one of the founding pillars of NLP (Natural Language Processing). We now define five main categories of phrases that are valid in the English language (but not only), with the help of the [Cambridge Dictionary](https://dictionary.cambridge.org). 

## Phrase classes
**NOUN PHRASE (NP)**
A noun phrase consists of a noun or pronoun, which is called the head, and any dependent words before or after the head. Dependent words give specific information about the head. Noun phrases can refer to a particular example of something or to a whole class of people or things.

**VERB PHRASE (VP)**
A verb phrase consists of a main verb alone, or a main verb plus any modal and/or auxiliary verbs. A simple verb phrase consists of a main verb. The verb in a simple verb phrase shows the type of clause (e.g. declarative, imperative). A complex verb phrase may include one modal verb and one or more auxiliary verbs before the main verb. A modal verb always comes before any auxiliary verbs.

**ADJECTIVE PHRASES (ADJP)**
An adjective phrase always has an adjective acting as the head. The adjective phrase may also contain words or phrases before or after the head (modifiers and complements). 

**ADVERB PHRASE (ADVP)**
An adverb phrase can consist of one adverb or an adverb plus other words before it (premodification) or after it (postmodification). Adverb phrases have many different meanings.

**PREPOSITIONAL PHRASE (PP)**
Prepositional phrases consist of a preposition and the words which follow it (a complement). The complement (underlined below) is most commonly a noun phrase or pronoun, but it can also be, an adverb phrase (usually one of place or time), a verb in the -ing form or, less commonly, a prepositional phrase or a wh-clause.

## NLTK implementation
Ready to code? Now we can see how to classificate phrases with NLTK library for python. Here the code:
```python
def phrases_classification(sentence):
    # Define grammar
    grammar = '''
              NP:{<DT>?<JJ>?<NN.*>}
              ADJP: {<JJ>}
              ADVP: {<RB.*>}
              PP: {<IN>}
              VP: {<MD>?<VB.*>+}  
            '''

    # Retrieve POS tag
    pos = nltk.pos_tag(sentence.split())

    # Use NLTK Regex to do the classification
    rxp = nltk.RegexpParser(grammar)
    classified_sentence = rxp.parse(pos)

    for item in classified_sentence:
        print(item)
```

To use the **phrases_classification** function, use this sample code:

```python
if __name__ == "__main__":
    sample_sentence = "To make lemonade, you have to start with lemons"

    print("---")
    print("Phrases Classification with NLTK")
    print("---\n")
    print("The sample sentence is: \n{}\n".format(sample_sentence))
    print("The classification is:")

    phrases_classification(sample_sentence)
```


Now you can play with phrase classification with NLTK!

