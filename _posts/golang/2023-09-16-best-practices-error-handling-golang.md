---
layout: post
title: "Error Handling in Go"
tags: ["go", "error"]
---

By convention, errors are the last return value of a function and have type `error` (a built-in interface).

```go
type error interface {
    Error() string
}
```

Usually, returning an error means that there is a problem, and returning nil means there were no errors:

```go
import "errors"

func iterate(x, y int) (int, error) {
	if arg == 42 {
		return -1, errors.New("can't work with 42")
	}
	return arg + 3, nil
}

result, err := iterate(x, y)
if err != nil {
	// handle the error appropriately
} else {
	// you're good to go
}
```

## Custom Errors

It’s possible to use custom types as errors by implementing the Error() method on them. Here’s a variant on the example above that uses a custom type to explicitly represent an argument error.

The two loops below test out each of our error-returning functions. Note that the use of an inline error check on the if line is a common idiom in Go code.

If you want to programmatically use the data in a custom error, you’ll need to get the error as an instance of the custom error type via type assertion.

```go
type argError struct {
    arg  int
    prob string
}

func (e *argError) Error() string {
    return fmt.Sprintf("%d - %s", e.arg, e.prob)
}
func f2(arg int) (int, error) {
    if arg == 42 {
    	return -1, &argError{arg, "can't work with it"}
    }
    return arg + 3, nil
}
func main() {

	    for _, i := range []int{7, 42} {
        if r, e := f1(i); e != nil {
            fmt.Println("f1 failed:", e)
        } else {
            fmt.Println("f1 worked:", r)
        }
    }
    for _, i := range []int{7, 42} {
        if r, e := f2(i); e != nil {
            fmt.Println("f2 failed:", e)
        } else {
            fmt.Println("f2 worked:", r)
        }
    }
    _, e := f2(42)
    if ae, ok := e.(*argError); ok {
        fmt.Println(ae.arg)
        fmt.Println(ae.prob)
    }
}
```

Code output:

```
$ go run errors.go
f1 worked: 10
f1 failed: can't work with 42
f2 worked: 10
f2 failed: 42 - can't work with it
42
can't work with it
```

## Defer, panic, and recover

In Go, the panic and recover functions are used for handling unexpected errors and recovering from them. The panic function is used to raise an error condition, and the recover function is used to catch and handle the panic.

Here's an example that demonstrates the use of panic and recover in Go:


```go
package main

import (
    "fmt"
)

func recoverPanic() {
    if r := recover(); r != nil {
        fmt.Println("Recovered from panic:", r)
    }
}

func main() {
    defer recoverPanic()

    panic("Oops! Something went wrong.")
}
```

In this example, the `recoverPanic` function is used to recover from a panic that occurs in the `main` function. The `defer` keyword is used to ensure that `recoverPanic` is called when a panic occurs. The `recover` function is used to recover from the panic and handle it gracefully.

> Defer puts your function call into a stack. Each deferred function is executed in reverse order when the host function finishes, regardless of whether a panic is called or not. 

https://blog.logrocket.com/error-handling-golang-best-practices/