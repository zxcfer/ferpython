---
layout: post
title: "Go Interfaces"
tags: ["go"]
---

## What is an interface?

- A type that specifies a set of method signatures.
- You **implement** an interface when you define all their methods.

## Definition

- Using the `type` keyword, the interface name and the `interface` keyword.

```go
type Writer interface {
    Write([]byte) (int, error)
}
```

## Embedding

Embedding allows one struct type to include another struct, inheriting the fields and methods of the embedded type.

```go
type Address struct {
    Street, City, State string
}

type Person struct {
    Name string
    Address
}

p := Person{
    Name:    "Kevin",
    Address: Address{"123 Pasos St", "Texcoco", "TX"},
}

fmt.Println(p.Street)  // Output: 123 Pasos St
```

In the example `Person` has a `Name`, `Street`, `City` and `State` due to the embedded Address.

## Inheritance 

Embedding provides a way to "inherit" methods. If the embedded type has methods, the embedding type will have those methods too, provided it doesn't define its own methods with the same name.

```go
func (a Address) FullAddress() string {
    return a.Street + ", " + a.City + ", " + a.State
}

// Even though Person doesn't define FullAddress, it gains the method through embedding Address.
address := p.FullAddress()
```


## POO

```go
package main

import (
	"fmt"
	"math"
)

type Circle struct {
	Radius float64
}

func (c Circle) Area() float64 {
	return math.Pi * math.Pow(c.Radius, 2)
}

func (c Circle) String() string {
	return fmt.Sprintf("Circle {Radius: %.2f}", c.Radius)
}

type Square struct {
	Width  float64
	Height float64
}

func (s Square) Area() float64 {
	return s.Width * s.Height
}

func (s Square) String() string {
	return fmt.Sprintf("Square {Width: %.2f, Height: %.2f}", s.Width, s.Height)
}

type Sizer interface {
	Area() float64
}

type Shaper interface {
	Sizer
	fmt.Stringer
}

func Less(s1, s2 Sizer) Sizer {
	if s1.Area() < s2.Area() {
		return s1
	}
	return s2
}

func PrintArea(s Shaper) {
	fmt.Printf("area of %s is %.2f\n", s.String(), s.Area())
}

func main() {
	c := Circle{Radius: 10}
	PrintArea(c)

	s := Square{Height: 10, Width: 5}
	PrintArea(s)

	l := Less(c, s)
	fmt.Printf("%v is the smallest\n", l)

}
```