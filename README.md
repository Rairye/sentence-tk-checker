# sentence-tk-checker
Checks output of an English sentence tokenizer and modifies the output according to default or user-defined rules.

This package can be useful if you are unable to modify your current English sentence tokenizer. (Unable to change parameters, retrain the tokenizer, etc.)

There are two primary ways of checking the results of the tokenizer.

1. Passing tokenized sentences to the class instance directly
2. Assigning the tokenizer’s tokenization function to the class instance


## Passing tokenized sentences to the class instance directly
```python

#This sample uses nltk, but you are free to use another tokenizer.
from nltk.tokenize import PunktSentenceTokenizer
from nltk.corpus import webtext

#The checker does not include a tokenizer.
from sentence_tk_checker.tokenizer_checker import checker

#Intiailizing a tokenizer. You are free to use your own method.
training_text = webtext.raw('overheard.txt')
tokenizer = PunktSentenceTokenizer(training_text)

#Intializing an instance of the checker class
w = checker()

#Assigning the tokenize() function of the tokenizer class to the checker instance 
w.set_function(tokenizer.tokenize)

source = "This is my source sentence. You are free to replace this with another one. Have a nice day."

sentences = w.tokenize(source)

for sentence in sentences:
    print(sentence)
```

## Assigning the tokenizer’s tokenization function to the class instance

```python
#This sample uses nltk, but you are free to use another tokenizer.
from nltk.tokenize import PunktSentenceTokenizer
from nltk.corpus import webtext

#The checker does not include a tokenizer.
from sentence_tk_checker.tokenizer_checker import checker

#Intiailizing a tokenizer. You are free to use your own method.
training_text = webtext.raw('overheard.txt')
tokenizer = PunktSentenceTokenizer(training_text)

#Intializing an instance of the checker class
w = checker()

source = "This is my source sentence. You are free to replace this with another one. Have a nice day."

#Using the tokenizer to tokenized the source text.
tokenized = tokenizer.tokenize(source)

#The results from the tokenizer are passed to the join_sentences method of the checker instance.
sentences = w.join_sentences(tokenized)

for sentence in sentences:
    print(sentence)

```
