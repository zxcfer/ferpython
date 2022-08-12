---
layout: post
title: "Semantic Similarity"
tags: ["nlp"]
---

```py
import spacy
nlp = spacy.load('en')

text = open('customer_feedback_627.txt').read()
doc = nlp(text)

for entity in doc.ents:
    print(entity.text, entity.label_)

# Determine semantic similarities
doc1 = nlp(u'the fries were gross')
doc2 = nlp(u'worst fries ever')
doc1.similarity(doc2)

# Hook in your own deep learning models
nlp.add_pipe(load_my_model(), before='parser')
```
