---
layout: post
title: "Don't Use Math.random() to Generate Random Numbers!"
tags: ["javascript", "typescript", "random", "crypto"]
---

![Dices](https://i.imgur.com/dSkeVXg.png)

Have you ever used `Math.random()` in JavaScript to generate random numbers? Well, you might want to reconsider that approach.

Math.random() is a built-in JavaScript function that returns a pseudo-random number between 0 and 1. While it can be useful in some cases, it has several limitations and drawbacks when it comes to generating truly random numbers.

```js
// a number from 0 to <1
console.log(Math.random());
```

## Deterministic algo

First off, `Math.random()` uses a deterministic algorithm, meaning that the sequence of numbers it generates is predictable and can be repeated if you know the starting point or "seed" value[^1]. This makes it unsuitable for applications that require a high level of security or unpredictability, like cryptography or gaming.

## Not friendly

Secondly, `Math.random()` has a limited range of output values. It can only generate numbers between 0 and 1, which means you'll need to perform additional calculations to get random integers or numbers within a specific range. This can lead to biases and uneven distributions, especially if not done correctly.

```js
// 0, 1 or 2
let randy = Math.floor(Math.random() * 3);
console.log(randy); 
```

## The Solution

So, what's the alternative? Well, modern browsers and Node.js provide more secure and reliable methods for generating random numbers, such as the Web Crypto API or the crypto module in Node.js. These use hardware-based random number generators or cryptographically secure pseudo-random number generators, which are much harder to predict and offer better statistical properties.

```js
const crypto = require("crypto");

// Random integers less than 100
let rand1 = crypto.randomInt(100);

// Random integers in range 20-80
let rand2 = crypto.randomInt(20, 80);
```

## Final thoughts

In conclusion, while Math.random() might seem convenient, it's not the best choice for applications that require truly random numbers. Consider using more secure and reliable alternatives, like the Web Crypto API or the crypto module in Node.js, to ensure the best possible randomness and security for your applications.

Remember, true randomness is crucial in many areas, so it's worth taking the time to do it right!

[^1]: [Why is Math.random() not designed to be cryptographically secure?](https://security.stackexchange.com/questions/181580/why-is-math-random-not-designed-to-be-cryptographically-secure).
