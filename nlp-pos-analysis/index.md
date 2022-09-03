# [NLP] Pos Analysis


## Intro

To allow a machine to understand human language, the components of each sentence must be categorized. One of the basic classification systems is the POS (part-of-speach), natively integrated into the nltk library. These tags give each component of the sentence a grammatical meaning.

## NLTK POS tags:

| Abbreviation | Meaning                                              
|--------------|------------------------------------------------------
| CC           | coordinating conjunction                             
| CD           | cardinal digit                                       
| DT           | determiner                                           
| EX           | existential there                                    
| FW           | foreign word                                         
| IN           | preposition/subordinating conjunction                
| JJ           | This NLTK POS Tag is an adjective (large)            
| JJR          | adjective, comparative (larger)                      
| JJS          | adjective, superlative (largest)                     
| LS           | list market                                          
| MD           | modal (could, will)                                  
| NN           | noun, singular (cat, tree)                           
| NNS          | noun plural (desks)                                  
| NNP          | proper noun, singular (sarah)                        
| NNPS         | proper noun, plural (indians or americans)           
| PDT          | predeterminer (all, both, half)                      
| POS          | possessive ending (parent\ ‘s)                       
| PRP          | personal pronoun (hers, herself, him, himself)       
| PRP$         | possessive pronoun (her, his, mine, my, our )        
| RB           | adverb (occasionally, swiftly)                     
| RBR          | adverb, comparative (greater)      
| RBS          | adverb, superlative (biggest)                        
| RP           | particle (about)                                   
| TO           | infinite marker (to)                                 
| UH           | interjection (goodbye)                               
| VB           | verb (ask)                                           
| VBG          | verb gerund (judging)                                
| VBD          | verb past tense (pleaded)                            
| VBN          | verb past participle (reunified)                     
| VBP          | verb, present tense not 3rd person singular(wrap)    
| VBZ          | verb, present tense with 3rd person singular (bases) 
| WDT          | wh-determiner (that, what)                           
| WP           | wh- pronoun (who)                                    
| WRB          | wh- adverb (how)                                     


## Code
Let's do a test with a short script. To run it you need the pip package and the downloader for NLTK. You can find information about the downloader in [this article](https://www.gslf.it/nlp-nltk-downloader/).

```python
import nltk

def pos_tags(sentence):
    tags = nltk.pos_tag(sentence.split())

    for tag in tags:
        print("[{}] {}".format(tag[1], tag[0]))

if __name__ == "__main__":
    sample_sentence = "The brown fox is quick and he is jumping over the lazy dog"
    pos_tags(sample_sentence)
```

The result is this:
```
[DT] The
[JJ] brown
[NN] fox
[VBZ] is
[JJ] quick
[CC] and
[PRP] he
[VBZ] is
[VBG] jumping
[IN] over
[DT] the
[JJ] lazy
[NN] dog
```

## Repo
You can find the basecode my [NLP GitHub repo](https://github.com/gslf/NaturalLanguageProcessing).

