---
layout: post
title: "NLTK sentences tokenizer"
tags: ["nltk", "tokenize"]
---

```py
from nltk.tokenize import sent_tokenize

text = "this's a sent tokenize test. this is sent two. is this sent three? sent 4 is cool! Now it's your turn."

sent_tokenize_list = sent_tokenize(text)
len(sent_tokenize_list) # 5
sent_tokenize_list
# ["this's a sent tokenize test.", 
#  'this is sent two.', 
#  'is this sent three?', 
#  'sent 4 is cool!', 
#  "Now it's your turn."]


import nltk.data
tokenizer = nltk.data.load('tokenizers/punkt/english.pickle')
tokenizer.tokenize(text)
# ["this's a sent tokenize test.", 
#  'this is sent two.', 
#  'is this sent three?', 
#  'sent 4 is cool!', 
#  "Now it's your turn."]

# Here is a spanish sentence tokenize example:
spanish_tokenizer = nltk.data.load('tokenizers/punkt/spanish.pickle')
spanish_tokenizer.tokenize('Hola amigo. Estoy bien.')
# ['Hola amigo.', 'Estoy bien.']
```