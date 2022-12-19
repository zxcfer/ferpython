---
layout: post
title: "Text to Vector"
tags: ["nlp"]
---

* Generating Vectors Using TF-IDF

TF-IDF frequency-inverse document frequency method for weighting the word value instead of simply counting it. It is used to determine how important a word is to a text within a collection documents.

TF-IDF is a bag-of-words (BoW) representation of the text that describes the occurrence of words within a text corpus. It doesn’t account for the sequence of the words. I’ll talk more about the limitations in the next section…

TextHero makes it easy to apply TF-IDF to the text in the dataframe.

```py
df['tfidf'] = (hero.tfidf(df['clean_text'], max_features=3000))
```

