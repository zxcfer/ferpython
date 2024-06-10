---
layout: post
title: "Go Types"
tags: ["go"]
---

buffer.md

https://www.educba.com/golang-buffer/

We can read the length of the string with the len function, which will return the numeric length, but what if the strings are too large?

- We want to calculate in the form of chunks of data, so in such situations, we can use the buffer; the buffer allows us to handle any size of the dynamic length, making it flexible.

The buffer name itself clarifies its purposes; it allows us to give buffer storage where we can store some data and access the same data when needed. 

1. To use the buffer in the go language, we need to import the bytes package of the go language.
2. Once we have imported the bytes package, we can create a variable with the byte package like var x =bytes. Buffer, and on the variable x, we can perform all the operations related to the buffering of string.
3. We can store data of string onto the buffer variable x like x.WriteString(“string of message ”), and the data which we stored on the string can be accessed like x.String().
4. We can check the length of the string stored on the buffer variable which we have created.
5. Even we can store the bytes of data like x.Write([]byte(“Hello “)), and we can get the length of the stored value in the form of a number like x.len().

```go
package main
import (
	"fmt"
)
//importing the bytes package so that buffer can be used
import (
	"bytes"
)
func main() {
//Creating buffer variable to hold and manage the string data
	var strBuffer bytes.Buffer
	strBuffer.WriteString("Ranjan")
	strBuffer.WriteString("Kumar")
	fmt.Println("The string buffer output is",strBuffer.String())
}
```

```out
output FerVas
```

asdasda


```go
package main
import (
	"fmt"
)
//importing the bytes package so that buffer can be used
import (
	"bytes"
)

func main() {
	//Creating buffer variable to hold and manage the string data
	var strBuffer bytes.Buffer
	fmt.Fprintf(&strBuffer, "It is number: %d, This is a string: %v\n", 10, "Bridge")
	strBuffer.WriteString("[DONE]")
	fmt.Println("The string buffer output is",strBuffer.String())
}
```

