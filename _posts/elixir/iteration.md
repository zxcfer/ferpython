---
layout: post
title: "Iteration in Elixir"
tags: ["elixir"]
---

iteration.md

## 

```ruby
def concat_messages(items) do
  items
  |> Enum.filter(&Item.ok?/1)
  |> Enum.reduce("", &(&2 <> Item.message(&1))
end

numbers = [12, 3, 7, -2, 4]

transformed_numbers = numbers
  |> Enum.with_index()
  |> Enum.map(fn {index, number} -> number * index end)
```

// The result is [0, 3, 14, -6, 16]

##

```ruby
def process_selection(prev_selection) when selection == 3

end

def process_selection(prev_selection \\ nil)
  selection = get_selection()
  do_something(selection)
  process_selection(selection)
end
```


```ruby
def fetch_something(i \\ 0)
  # http request
end

def fetch_something(i) when i < 5 do
  case make_external_http_call do
    {200, body} -> body
    {_status, _body} -> fetch_something(tries + 1)
  end
end

def fetch_something(i) when i >= 5 do
  "Service not available"
end
```