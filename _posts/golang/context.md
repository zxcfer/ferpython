---
layout: post
title: "Go Contexts"
tags: ["go"]
---

https://code.tutsplus.com/es/context-based-programming-in-go--cms-29290t
https://articles.wesionary.team/understanding-context-package-in-golang-ed62f14edf6a


* Go programs that run multiple simultaneous calculations in goroutines need to manage their durability.
* Runaway goroutines can enter infinite loops, block other waiting goroutines, or simply take too long.
* Ideally you should be able to cancel goroutines or have them paused in some way.

Enter content-based programming. Go 1.7 introduced the context package, which offers precisely those capabilities, as well as the ability to associate arbitrary values ​​with a context that travels with the execution of requests and allows out-of-band communication and information passing.

El contexto te permite encapsular información que no es relevante para el cálculo principal, como la
- identificación de la solicitud, 
-el token de autorización y 
- el tiempo de espera. 

Existen varios beneficios de esta encapsulación:

- Separa los parámetros de cálculo centrales de los parámetros operativos.
- Codifica aspectos operativos comunes y cómo comunicarlos a través de los límites.
- Ofrece un mecanismo estándar para añadir información fuera de banda sin cambiar las firmas.

 cancellation and data sharing

## Context Interface

```go
type Context interface {
  Deadline() (deadline time.Time, ok bool)
      Done() <-chan struct{}
	   Err() error
     Value(key interface{}) interface{}
}
```

1. The Deadline field returns the expected time the work is finished and indicates when the context should be canceled.

2. The Done field is a channel that is closed when work done for the context should be canceled. This operation can happen asynchronously. The channel can return as nil if the associated context can never be canceled. Different context types will arrange for work to be canceled depending on the circumstances, which we will get into.

3. Err will return nil until Done is closed. After which Err will either return Canceled if the context was canceled or DealineExceeded if the context’s deadline has passed.

4. The Value field is a key-value interface which will return a value associated with the context as a key or nil if there was no value associated. Values should be used carefully as they are not for passing parameters into a function but for request-scoped data transits processes and API boundaries.

## Ámbito (scope) de context

Los contextos tienen ámbitos (scopes). Puedes derivar ámbitos de otros ámbitos, y el ámbito principal no tiene acceso a los valores de los ámbitos derivados, pero los ámbitos derivados tienen acceso a los valores de los ámbitos principales.

Los contextos forman una jerarquía. Comienzas con context.Background() o context.TODO(). Cada vez que llamas a WithCancel(), WithDeadline() o WithTimeout(), creas un contexto derivado y recibes una función de cancelación. Lo importante es que cuando un contexto principal se cancela o caduca, todos sus contextos derivados.

Debes utilizar context.Background() en la función main(), en las funciones init() y en las pruebas. Debes usar context.TODO() si no está seguro de qué contexto utilizar.

Ten en cuenta que Background y TODO no se pueden cancelar.

The “Background” function returns an empty non-nil context. There is no associated deadline and no cancelation to speak of. This can be typically used in the main function, for testing, or for creating a top-level context to be made into something else. 

Context.TODO
The TODO function does the same thing. It returns an empty non-nil context. This again is a use case for higher-level functions that may not yet have a function available to use them. In many cases, this would be used as a placeholder when extending your program to use the context library.


## DErivados

Deadlines, timeouts y cancelaciones
Como recordarás, WithDeadline() y WithTimeout() devuelven contextos que se cancelan automáticamente, mientras que WithCancel() devuelve un contexto y debe ser cancelado explícitamente. Todos ellos devuelven una función de cancelación, así que aunque timeout/deadline no haya expirado todavía, aún puedes cancelar cualquier contexto derivado.

Examinemos un ejemplo. Primero, aquí está la función contextDemo() con un nombre y un contexto. Se ejecuta en un bucle infinito, imprimiendo a la consola su nombre y el plazo de su contexto si lo hay. Luego, solo se suspende por un segundo.

```go
package main 
import (
    "fmt"
    "context"
    "time"
)

func contextDemo(name string, ctx context.Context) {    
    for {
        if ok {
            fmt.Println(name, "will expire at:", deadline)
        } else {
            fmt.Println(name, "has no deadline")
        }
        time.Sleep(time.Second)
    }
}

func main() {
    timeout := 3 * time.Second
    deadline := time.Now().Add(4 * time.Hour)

    timeOutContext, _ := context.WithTimeout(
        context.Background(), timeout)
    
    cancelContext, cancelFunc := context.WithCancel(
        context.Background())
    
    deadlineContext, _    := context.WithDeadline(
        cancelContext, deadline)
    
    go contextDemo("[timeoutContext]", timeOutContext)
    go contextDemo("[cancelContext]", cancelContext)
    go contextDemo("[deadlineContext]", deadlineContext)
    
    // Wait for the timeout to expire
    <- timeOutContext.Done()
    
    // This will cancel the deadline context as well as its
    // child - the cancelContext
    fmt.Println("Cancelling the cancel context...")
    cancelFunc()
    <- cancelContext.Done()
    
    fmt.Println("The cancel context has been cancelled...")
    
    // Wait for both contexts to be cancelled
    <- deadlineContext.Done()
    fmt.Println("The deadline context has been cancelled...")
}

```

```
[cancelContext] has no deadline
[deadlineContext] will expire at: 2017-07-29 09:06:02.34260363
[timeoutContext] will expire at: 2017-07-29 05:06:05.342603759
[cancelContext] has no deadline
[timeoutContext] will expire at: 2017-07-29 05:06:05.342603759
[deadlineContext] will expire at: 2017-07-29 09:06:02.34260363
[cancelContext] has no deadline
[timeoutContext] will expire at: 2017-07-29 05:06:05.342603759
[deadlineContext] will expire at: 2017-07-29 09:06:02.34260363
Cancelling the cancel context...
The cancel context has been cancelled...
The deadline context has been cancelled...
```

## value

- Puedes adjuntar valores a un contexto utilizando la función WithValue().
- Observa que se devuelve el contexto original, no un contexto derivado.

```go
func contextDemo(ctx context.Context) {
    deadline, ok := ctx.Deadline()
    name := ctx.Value("name")
    for {
        if ok {
            fmt.Println(name, "will expire at:", deadline)
        } else {
            fmt.Println(name, "has no deadline")
        }
        time.Sleep(time.Second)
    }
}
```

Y modifiquemos la función principal para adjuntar el nombre mediante WithValue():

```go
go contextDemo(context.WithValue(
    timeOutContext, "name", "[timeoutContext]"))
go contextDemo(context.WithValue(
    cancelContext, "name", "[cancelContext]"))
go contextDemo(context.WithValue(
    deadlineContext, "name", "[deadlineContext]"))
```

El resultado sigue siendo el mismo. Revisa la sección de las mejores prácticas para obtener algunas pautas sobre el uso adecuado de los valores de contexto.

## There are also some notes about context:

Do not store Contexts in struct types, but pass the Context explicitly to each function that needs it, and the Context should be the first argument.
Do not pass a nil Context, even if the function allows it, or if you are not sure which Context to use, pass context.
Do not pass variables that could be passed as function arguments to the Value of the Context.
