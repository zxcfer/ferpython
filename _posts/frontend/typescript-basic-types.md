---
layout: post
title: "Typescript Basic Types"
tags: ["typescript"]
---

Typescript has basically 5 categories of types.

* Primitives
* Literals
* Data Structures
* Unions
* Intersections

## Primitive types

```ts
// número
let num: number = 10;

// string
let str: string = 'hello';

// boolean
let isLogin: boolean = false;

// bigint
const y = BigInt(10);

// appending n to the end of an integer literal
const x = 10n;

// symbol values are created by calling the Symbol constructor.
let sym1 = Symbol();
let sym2 = Symbol("key"); // optional string key

// undefined
// null: discouraged
```

## Literal types

Here literal means exactly that, the type is is exactly the value you see.

```ts
const ten: 10 = 10;
const hello: \`hello\` = \`hello\`;
```

That is, the variable ten has as type the number 10, so it can only contain as value the number 10. The same with the variable hello, the only value it can have is the string hello since the type annotation indicates that it is the literal string hello.

## Data Structures

```ts
// Objects: A type that describes the "shape" of an object as a finite set of key:value pairs.
type Object = {
  name: string;
  age: number;
}

// An object whose property names are strings but whose type Record = { [key: string]: unknown} value is unknown.
type Record2 = Record<string, unknown> // Identical result to previous line
type Tuple = [string, number, boolean] // A finite set of 3 elements 
type Arr = Array<string> // An infinite array of just strings, can also be written as string[].

// arrays
const arr: Array<string> = [];

// 
const items: string[] = [];

// tuple
const address: [string, number] = ['age', 40];

// object
const obj: object = {};
```

## Unions and Intersections

```ts
type Union = X | Y 
type Intersection = X & Y 
```