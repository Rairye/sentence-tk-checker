# sentence-tk-checker
Checks output of an English sentence tokenizer and modifies the output according to default or user-defined rules.

## Why use this package?

This package can be useful if you are unable to modify your current English sentence tokenizer. (Unable to change parameters, retrain the tokenizer, etc.)


### Novel abbreviation detection

The package includes a function for detecting possible novel abbreviations. (Enabled by default. For more information, see https://github.com/Rairye/sentence-tk-checker/wiki/Customization)

### User settings

Users can customize: abbreviations, titles, abc characters, vowel characters, puntuation characters, and sentence-end punctuation characters. (For more information, see https://github.com/Rairye/sentence-tk-checker/wiki/Customization)

### Fragment detection

Detects possible sentence fragments.

There are two primary ways of checking the results of the tokenizer that you are using.

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

## Customization

For more information about customizations, please check the wiki:

https://github.com/Rairye/sentence-tk-checker/wiki/Customization

## Computational Complexity

The checker does not check the entires contents of every sentence returned by the tokenizer. Rather, it is inspects the boundaries of the sentences and join certain sentences (possible sentence fragments) together.

## Notes 

1. This package is optimized for English and has not been tested with other languages.
2. This package assumes that proper punctuation is used in the text.
