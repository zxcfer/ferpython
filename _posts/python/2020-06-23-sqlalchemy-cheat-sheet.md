---
layout: post
title: "SQLAlchemy"
tags: ["python", "orm"]
---
---
layout: post
title:  "SQLAlchemy"
description: this article explains something and gives a brief introduction.
tags: welcome introduction
---


```py
db.Column(db.BigInteger)
Boolean
```

Column(DateTime, default=datetime.datetime.utcnow)

### Links

* Full cheat sheet https://www.pythonsheets.com/notes/python-sqlalchemy.html
* Table relation https://hackersandslackers.com/sqlalchemy-data-models/
* CRUD https://medium.com/@allwindicaprio/crud-operations-using-flask-and-sqlalchemy-7291e340dcc8


```py
book = Book(name="The monk who", author="Robin Sharma", published="1997-03-04")
session.add(book)
session.commit()

session.delete(book)
session.commit()
```

Quering

```python
book = Book.query.all()
book = Book.query.get(1)

session.query(User).filter(User.age == 25)
query = session.query(User).order_by(User.id)
query = session.query(User).order_by(desc(User.id))
query = session.query(User).order_by(User.birth)
query = session.query(User).filter(User.id==2)
_row = query.first()
query = session.query(User).filter(User.id!=2)
query = session.query(User).filter(User.name.in_(['ed', 'wendy']))
query = session.query(User).filter(~User.name.in_(['ed', 'wendy']))
query = session.query(User).filter(User.name=='ed', User.fullname=='Ed Jones')
_row = query.first()

query = session.query(User).filter(or_(User.name=='ed', User.name=='wendy'))
query = session.query(User).filter(User.birth == None)
query = session.query(User).filter(User.birth != None)
query = session.query(User).filter(User.name.like('%ed%'))
```

