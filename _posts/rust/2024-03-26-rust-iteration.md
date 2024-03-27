---
layout: post
title: "Iteration in Rust"
tags: ["iteration", "rust"]
---

Rust provides several ways to iterate over collections or ranges of values. Here are the main iteration methods and when to use them:

1. **`for` loop**:
This is the most common way to iterate over an iterator. It is used when you want to perform an operation on each element of a collection or range.

```rust
let numbers = vec![1, 2, 3, 4, 5];
for num in numbers.iter() {
    println!("{}", num);
}
```

2. **`iter()` and `iter_mut()`**:
These methods are used to create an iterator over the elements of a collection. `iter()` returns an immutable iterator, while `iter_mut()` returns a mutable iterator.

```rust
let mut numbers = vec![1, 2, 3, 4, 5];
for num in numbers.iter_mut() {
    *num *= 2; // Modifying the elements
}
```

3. **`into_iter()`**:
This method consumes the collection and returns an iterator that owns the elements. It is useful when you want to iterate over a collection and potentially modify or consume its elements.

```rust
let numbers = vec![1, 2, 3, 4, 5];
for num in numbers.into_iter() {
    println!("{}", num);
}
// `numbers` is no longer available here
```

4. **`enumerate()`**:
This method returns an iterator that yields tuples containing the index and the value of each element in the collection.

```rust
let numbers = vec![1, 2, 3, 4, 5];
for (index, num) in numbers.iter().enumerate() {
    println!("Index: {}, Value: {}", index, num);
}
```

5. **`zip()`**:
This method is used to iterate over two iterators simultaneously, yielding pairs of elements from each iterator.

```rust
let numbers1 = vec![1, 2, 3];
let numbers2 = vec![4, 5, 6];
for (num1, num2) in numbers1.iter().zip(numbers2.iter()) {
    println!("{} + {} = {}", num1, num2, num1 + num2);
}
```

6. **Range expressions**:
Rust provides a concise way to iterate over a range of values using range expressions (`start..end` or `start..=end`).

```rust
for i in 0..5 {
    println!("{}", i);
}
```

7. **`while` loop**:
While not strictly an iteration method, `while` loops can be used to iterate over iterators manually.

```rust
let mut iter = numbers.iter();
while let Some(num) = iter.next() {
    println!("{}", num);
}
```

The choice of which iteration method to use depends on your specific use case, whether you need to modify the elements, consume the collection, or iterate over multiple iterators simultaneously. The `for` loop and range expressions are generally the simplest and most common choices for basic iteration scenarios.