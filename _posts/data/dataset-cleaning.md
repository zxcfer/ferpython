---
layout: post
title: "Clearing datasets"
tags: ["nlp"]
---

Texthero is a python package to work with text data efficiently.
It empowers NLP developers with a tool to quickly understand any text-based dataset and
it provides a solid pipeline to clean and represent text data, from zero to hero.

```bash
pip install texthero
```

I'm going to use the Texthero library as it simplifies cleaning text in DataFrames

```py
hero.clean(pandas.Series)
```

```py
fillna(s) Replace not assigned values with empty spaces.
lowercase(s) Lowercase all text.
remove_digits() Remove all blocks of digits.
remove_punctuation() Remove all string.punctuation (!"#$%&'()*+,-./:;<=>?@[\]^_`{|}~).
remove_diacritics() Remove all accents from strings.
remove_stopwords() Remove all stop words.
remove_whitespace() Remove all white space between words.
```


## Custom cleaning

```py
import texthero as hero
from texthero import preprocessing
custom_pipeline = [preprocessing.fillna,
                   #preprocessing.lowercase,
                   preprocessing.remove_whitespace,
                   preprocessing.remove_diacritics
                   #preprocessing.remove_brackets
                  ]
```


[1]: https://texthero.org/