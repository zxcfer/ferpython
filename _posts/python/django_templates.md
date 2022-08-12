---
layout: post
title: ""
tags: [""]
---

## Django Templates

```html
{% if error %}
	<p style="color: red;">Please submit a search term.</p>
{% endif %}
<form action="/search/" method="get">
	<input type="text" name="q">
	<input type="submit" value="Search">
</form>
```

```html
	<!-- For and If statements -->
	<ul>
	{% for object in objects %}
	  {% if forloop.first %}
		<li class="first">
	  {% else %}
		<li>
	  {% endif %}
	  {{ object }}
	  </li>
	{% endfor %}
	</ul>
```

* Nice menu example:

```php
{% for link in links %} {{ link }}
	{ % if not forloop.last %} | { % endif %}
{% endfor %}
```

* For key/value statements

```php
	{% for k, v in defaultdict.iteritems %}
		Do something with k and v here...
	{% endfor %}
```

* Comparing variables

```php
{% ifequal variable 1 %}
{% ifequal variable 1.23 %}
{% ifequal section "community" %}
{% ifequal section 'sitenews' %}
{% ifequal user currentuser %}
	<h1>Welcome!</h1>
{% else %}
	<h1>No News Here</h1>
{% endifequal %}
```

* Filters

```php
{{ name|lower }}    			# lowercase the text
{{ bio|truncatewords:"3" }}  	# words! not characters
addslashes: Agrega una con contra-barra.
date: Formatea un objeto date o datetime {{ pub_date|date:"F j, Y" }}
escape: convierte caracteres especiales a xhtml

<p>You searched for: <strong>{{ query }}</strong></p>
{% if books %}
	<p>Found {{ books|length }} book{{ books|pluralize }}.</p>
	<ul>
		{% for book in books %}
		<li>{{ book.title }}</li>
		{% endfor %}
	</ul>
{% else %}
	<p>No books matched your search criteria.</p>
{% endif %}
```