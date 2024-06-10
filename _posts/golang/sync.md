---
layout: post
title: "Sync Golang"
tags: ["go"]
---

# sync.md

https://coffeebytes.dev/es/go-introduccion-a-las-goroutines-y-concurrencia/
https://levelup.gitconnected.com/go-a-benchmark-to-compare-synchronization-techniques-ed73e118ec35

## The problem

When each task executed by the computer cannot be further subdivided (it cannot be split into smaller subtasks), it is an atomic task.

Usually, num = num + 1 looks like a single line of code, but it actually adds num to 1 and then writes num, which is not an atomic operation since there are two instructions after compilation.

```go
import "sync"
func add(w *sync.WaitGroup, num *int) {
    defer w.Done()
    *num= *num + 1
}
func main() {
    var n int = 0
    var wg *sync.WaitGroup = new(sync.WaitGroup)
    wg.Add(1000)
    for i := 0; i < 1000; i = i + 1 {
	go add(wg, &n)
    } // spawn 1000 new goroutines
    wg.Wait()
    println(n)
}
```

## sync/atomic

- The `sync/atomic` package provides support for atomic operations for synchronizing reads and writes of integers and pointers.
- Types of operations: `add`, `subtract`, `compare` and `swap`, load, store, and swap.
- The types supported by atomic operations include `int32`, `int64`, `uint32`, `uint64`, `uintptr`, `unsafe.Pointer`.

For example, for the above example, replace `*num = *num + 1` with the atomic operation provided by the sync/atomic package:

```go
import "sync"
import "sync/atomic"

func add(w *sync.WaitGroup, num *int32) {
    defer w.Done()
    atomic.AddInt32(num, 1) // *num = *num + 1
}

func main() {
    var n int32 = 0
    var wg *sync.WaitGroup = new(sync.WaitGroup)
    wg.Add(1000)

    // create 1000 new goroutines
    for i := 0; i < 1000; i = i + 1 {
		go add(wg, &n)
    } 
    
    wg.Wait()
    println(n)
}
```

## sync.WaitGroup

- The `sync.WaitGroup` struct in the sync package is used to wait for a group of goroutines to finish executing, and control is blocked until the group of goroutines finishes executing.
- Each `sync.WaitGroup` value maintains an internal count, which initially defaults to zero.

For an addressable sync.WaitGroup value wg:

wg.Add(delta) to change the value of the count maintained by wg, wg.Done() and wg.Add(-1) are exactly equivalent
If a wg.Add(delta) or wg.Done() call changes the count maintained by wg to a negative number, a panic will be generated
When wg.Wait() is called by a goroutine if the count maintained by wg is zero, the wg.Wait() operation is a null operation; otherwise (the count is a positive integer), the goroutine will go into a blocking state, and when some other goroutine later changes the count to zero (typically by calling wg.Done()), the concurrent process will re-enter the running state (i.e. wg.Wait() will return)
For an example, see the sync/atomic example above. The main goroutine will go into a blocking state to wait for 1000 to complete, after which the main goroutine will unblock.

## sync.Mutex

- `Mutex value`: a mutex lock
- `Mutex zero value`: a mutex lock that has not yet been locked:

```go
var mutex *sync.Mutex = nil.
```

- If goroutine state is **unlocked**, call `m.Lock()` to change state to locked, call `m.Unlock()` will cause RuntimError exception.
- If the goroutine state is **locked**, `m.Lock()` will be blocked until another goroutine calls m.Unlock() to release the lock, and m.Unlock() to change the state to unlocked.

```go
import "sync"

var num int = 0

func add(lc *sync.Mutex, wg *sync.WaitGroup) {
    defer wg.Done()
    for i := 0; i < 100000; i = i + 1 {
        lc.Lock()        // block to be modified till unlock
        num = num + 1
        lc.Unlock()
    }
}

func minus(lc *sync.Mutex, wg *sync.WaitGroup) {
    defer wg.Done()
    for i := 0; i < 100000; i = i + 1 {
        lc.Lock()        // block goroutine
        num = num - 1
        lc.Unlock()      // release
    }
}

func main() {
    var mutex *sync.Mutex = new(sync.Mutex)
    var wg *sync.WaitGroup = new(sync.WaitGroup)
    
    wg.Add(2)
    go add(mutex, wg)
    go minus(mutex, wg)
    wg.Wait()
    
    println(num)       // Result is 0
}
```

## sync.RMutex


When a goroutine is writing, the other goroutines can neither read nor write.

`Mutex` and `sync.RWMutex` types both implement the sync:

```
type Locker interface {
    Lock()
    Unlock()
}
```

sync.RWMutex type has two other methods: RLock() and RUnlock().

So the total is:
- `func (rw *RWMutex) Lock()`: Get a write lock
- `func (rw *RWMutex) Unlock()`: release write lock
- `func (rw *RWMutex) RLock()`: Get a read lock
- `func (rw *RWMutex) RUnlock()`: release read lock

## sync.Cond

Unlike a mutex, a condition variable does not guarantee that only one goroutine has access to a shared data at the same time, but notifies other goroutines that are blocked when the state of the corresponding shared data changes.

Conditional variables are always used in combination with mutexes, which provide mutex support for accessing shared data, and conditional variables, which notify the relevant goroutine of a change in the state of the shared data.(That is, when defining variables with var cond `*sync.Cond = sync.NewCond(new(sync.Mutex)))`

After seizing a lock, it determines whether it satisfies the processing conditions, and if not, it releases the lock to other goroutines, then blocks itself, waits for other goroutines to notify it, then releases the block, and then goes back to acquire the lock.
For an addressable variable cond of type `*sync.Cond`, the following methods are commonly used:
cond.L.Lock() and cond.L.Unlock(): lock() and lock.Unlock() can also be used, exactly the same.
cond.Wait(): When this method is called, the outflow of the executed operation is: Unlock() -> blocking waiting notification (i.e. waiting for notification from Signal() or Broadcast()) -> receiving notification -> Lock().
cond.Signal(): Notify a Wait goroutine, if there is no Wait(), no error will be reported, Signal() notification order is based on the original join notification list (Wait()) first in first out.
cond.Broadcast(): Notify all Wait goroutines, if there is no Wait(), no error will be reported.
For example:

```go
func main() {
    var cond *sync.Cond = sync.NewCond(new(sync.Mutex))
    var condition int = 0
  
    // Consumer
    go func() {
        for {
            cond.L.Lock()
            for condition == 0 {
                cond.Wait()
            }
            condition = condition - 1
            println(condition)
            cond.Signal()
            cond.L.Unlock()
        }
    }()
    // Producer
    for {
        time.Sleep(time.Second)
        cond.L.Lock()
        for condition == 3 {
            cond.Wait()
        }
        condition = condition + 1
        println(condition)
        cond.Signal()
        cond.L.Unlock()
    }
}
```

## sync.Map

- IO for maps in Golang is not concurrently safe
- reading and writing maps between multiple goroutines will result in a fatal error: concurrent map writes.
- `sync.Map` solve this problem

For example:

```go
import "sync"

func run(wg *sync.WaitGroup, sc *sync.Map) {
    defer wg.Done()
    var sceneIterate func(interface{}, interface{}) bool = func(k interface{}, v interface{}) bool {
        println("iterate:", k, v)
        return true
    }
    sc.Range(sceneIterate)
}

func main() {
    var scene *sync.Map = new(sync.Map)
    
    scene.Store("greece", 97)
    scene.Store("london", 100)
    scene.Store("egypt", 200)
    var v interface{} = nil
    var ok bool = false
    v, ok = scene.Load("london")
    println(v, ok)
    scene.Delete("london")
    
    var wg *sync.WaitGroup = new(sync.WaitGroup)
   
    wg.Add(1)
    go run(wg, scene)
    wg.Wait()
}
```

## sync.Pool

- sync.Pool can be used to cache objects, since frequent use of heap memory can cause too much work for GC.

sync.Pool can be reclaimed without notice to relieve GC pressure.
To initialize the pool, the only thing you need is to set up the New function so that when the Get method is called, if the pool has a cached object, it returns the cached object directly, and if it does not, the New function is called to create a new object.
For example:

```go
import "sync"
var intPool *sync.Pool = &sync.Pool {
    New: func() interface{} {
        var b []int = make([]int, 8)
        return &b
    },
}
func main() {
    // get the obj and do not put it back
    for i := 1; i < 4; i = i + 1 {
        var obj *[]int = intPool.Get().(*[]int)
        (*obj)[i] = i
        println(obj)
    }
    println("=======")
    // get the obj and put it back
    for i := 1; i < 4; i = i + 1 {
        var obj *[]int = intPool.Get().(*[]int)
        (*obj)[i] = i
        println(obj)
        intPool.Put(obj)
    }
}
console:
0xc00000c060
0xc00000c080
0xc00000c0a0
=======
0xc00000c0c0
0xc00000c0c0
0xc00000c0c0
```

As you can see from the console, the structs fetched and put back are the same.
Pools are suitable for scenarios where there is a lot of memory and a lot of concurrency, but when there is little memory and little concurrency, using pools is counterproductive.
The best practice for using sync.Pool is: Empty Pool before Put, Empty Pool after Get.

## Channel

Finally, the Channel is used for much more than just synchronizing multiple goroutines, they are also used to pass data between different goroutines, or to control the number of goroutines, etc. The previous synchronization techniques can only be used to synchronize, which is where Channel differs from them.
In the absence of extreme cases, the use of Channel is preferred in synchronization techniques.

For the sync.Cond example above, it can be implemented as a Channel instead:

```go
func main() {
    var ch chan int = make(chan int, 3)
    var v int = 0
    // Consumer
    go func() {
        for {
            println(<- ch)
        }
    }()
    // Producer
    for {
        v = v + 1
        println(v)
        ch <- v
        time.Sleep(time.Second)
    }
}
```