## DATA TYPES

![image](https://github.com/user-attachments/assets/d7e72314-eaef-47fc-bd85-72440c5fbbfc)

---

## Packages
Every Go program is made up of packages.

Programs start running in package `main`.

---

## Type Inference

```go
v := 42
```

---

## For Loop

Go has several types of `for` loops:

1. **Standard for loop**:  
   ```go
   // init-condition-postStatement
   for i := 0; i < 10; i++ {
       sum += i
   }
   ```

2. **For loop with condition**:  
   ```go
   for ; sum < 1000; {
       sum += sum
   }
   ```

3. **For loop with only condition**:  
   ```go
   for sum < 1000 {
       sum += sum
   }
   ```

4. **Infinite loop**:  
   ```go
   for {
       // infinite loop
   }
   ```

5. **Using `range`**:  
   ```go
   var pow = []int{1, 2, 4, 8, 16, 32, 64, 128}
   
   func main() {
       for i, v := range pow {
           fmt.Printf("2**%d = %d\n", i, v)
       }
   }
   ```

---

## SWITCH

A switch statement is a shorter way to write a sequence of `if-else` statements.

- Go only runs the selected case, not all the cases that follow.
- The `break` statement that is needed at the end of each case in those languages is provided automatically in Go.
- Another important difference is that Go's switch cases need not be constants, and the values involved need not be integers.

Switch without a condition is the same as `switch true`.

```go
fmt.Print("Go runs on ")
switch os := runtime.GOOS; os {
case "darwin":
    fmt.Println("OS X.")
case "linux":
    fmt.Println("Linux.")
default:
    // freebsd, openbsd,
    // plan9, windows...
    fmt.Printf("%s.\n", os)
}
```

---

## DEFER

A `defer` statement defers the execution of a function until the surrounding function returns.

- The deferred call's arguments are evaluated immediately, but the function call is not executed until the surrounding function returns.
- When a function returns, its deferred calls are executed in last-in-first-out order.

```go
for i := 0; i < 10; i++ {
    defer fmt.Print(i)
}

// OUTPUT: 9876543210
```

---

## Pointers

A **pointer** holds the memory address of a value. Unlike C, Go has no pointer arithmetic.

```go
i, j := 42, 2701

p := &i         // point to i
fmt.Println(*p) // read i through the pointer
*p = 21         // set i through the pointer
fmt.Println(i)  // see the new value of i

p = &j          // point to j
*p = *p / 37    // divide j through the pointer
fmt.Println(j)  // see the new value of j
```

---

## Structs

A **struct** is a collection of fields.

```go
type Vertex struct {
    X int
    Y int
}

func main() {
    v := Vertex{1, 2}
    p := &v
    // p.X , (*p).X both can be used to get or update struct fields 
    p.X = 1e9
    fmt.Println(v)
    (*p).X = 23
    fmt.Println(v)
}
```

---

## Maps

A **map** maps keys to values. The zero value of a map is `nil`.

### Example:

The following will result in an error because a nil map cannot store any elements:

```go
package main

import "fmt"

var m map[string]int

func main() {
    // Remove the comment below, then it will work:
    // m = make(map[string]int)
    m["Bell Labs"] = 12
    fmt.Println(m["Bell Labs"])
}
```

**Error:**
```text
panic: assignment to entry in nil map
```

### Deleting an element:

```go
delete(m, "Bell Labs")
```

### Test if a key is present:

```go
elem, ok := m["Bell Labs"]
```

If the key is in `m`, `ok` will be `true`. If the key is not in the map, `ok` will be `false`, and `elem` will be the zero value for the map's element type.

---

## Function Closures

In Go, **closures** are functions that refer to variables defined outside of their scope. Closures allow you to maintain state between function calls, even after the outer function has returned.

### Example: Closure for Adder

```go
package main

import "fmt"

func adder() func(int) int {
	sum := 0
	return func(x int) int {
		sum += x
		return sum
	}
}

func main() {
	a := adder() // Closure 1
	b := adder() // Closure 2

	// Using closure a
	fmt.Println(a(11)) // Outputs: 11
	fmt.Println(a(11)) // Outputs: 22

	// Using closure b
	fmt.Println(b(11)) // Outputs: 11
}
```

### Where to Use:
- **Callbacks**: Functions that are passed into other functions and executed later.
- **Encapsulation of State**: Maintaining state without exposing it directly.

---

## Methods in Go

A **method** in Go is simply a function with a receiver argument. It defines behavior for types (usually structs).

### Value Receivers vs Pointer Receivers

1. **Pointer Receivers**: Methods that can modify the value of the receiver.
2. **Value Receivers**: Methods that do not modify the receiver but can work with its copy.

### Example: Method with Pointer Receiver

```go
package main

import "fmt"

type Vertex struct {
	X, Y float64
}

// Method with pointer receiver
func (v *Vertex) Scale(f float64) {
	v.X = v.X * f
	v.Y = v.Y * f
}

func main() {
	v := Vertex{3, 4}
	v.Scale(2) // OK, method modifies the receiver

	fmt.Println(v) // Outputs: {6 8}
}
```

### Example: Method with Value Receiver

```go
package main

import "fmt"
import "math"

type Vertex struct {
	X, Y float64
}

// Method with value receiver
func (v Vertex) Abs() float64 {
	return math.Sqrt(v.X*v.X + v.Y*v.Y)
}

func main() {
	v := Vertex{3, 4}
	fmt.Println(v.Abs()) // Outputs: 5
}
```

### Choosing Between Value or Pointer Receivers:
- **Use pointer receivers** if the method needs to modify the receiver’s state.
- **Use value receivers** for efficiency when dealing with small structs or if the method does not modify the receiver.

---

## Interfaces in Go

Interfaces in Go are **implicitly implemented**, meaning there’s no need to declare that a type implements an interface. A type implements an interface simply by having the methods required by the interface.

### Example: Interface Implementation

```go
package main

import "fmt"

type Stringer interface {
	String() string
}

type Person struct {
	Name string
	Age  int
}

func (p Person) String() string {
	return fmt.Sprintf("%s is %d years old", p.Name, p.Age)
}

func main() {
	p := Person{"Alice", 30}
	var s Stringer = p
	fmt.Println(s.String()) // Outputs: Alice is 30 years old
}
```

### Nil Interface Values
A **nil interface value** holds no value and no concrete type. Attempting to call a method on a nil interface will result in a runtime panic.

### Type Assertions
Type assertions allow you to extract the underlying value from an interface.

```go
var i interface{} = "hello"
s := i.(string) // OK
fmt.Println(s) // Outputs: hello

// Panic example
i = 42
s := i.(string) // Panic: interface conversion: int is not string

// Safe assertion
s, ok := i.(string) // ok = false
fmt.Println(s, ok)   // Outputs:  false
```

### Type Switches

```go
switch v := i.(type) {
case string:
    fmt.Println("String:", v)
case int:
    fmt.Println("Int:", v)
default:
    fmt.Println("Unknown type")
}
```

---

## Empty Interface

In Go, the **empty interface** is an interface type that specifies **zero methods**. Since every type implements at least zero methods, all types in Go implement the empty interface.

### Usage
The empty interface can hold values of **any type**, making it useful when you don't know what type of value will be passed. For example, the `fmt.Print()` function accepts arguments of type `interface{}`, allowing it to print any type of value.

### Example: Using the Empty Interface

```go
package main

import "fmt"

func printAnything(value interface{}) {
	fmt.Println(value)
}

func main() {
	printAnything(42)        // Outputs: 42
	printAnything("Hello!")  // Outputs: Hello!
	printAnything([]int{1, 2, 3}) // Outputs: [1 2 3]
}
```

The empty interface is commonly used for accepting any type of data when you don't need to specify the type beforehand.

---

## Error Handling in Go

Errors are handled through the `error` interface. The `Error()` method must be implemented to represent an error message.

### Example: Handling Errors

```go
package main

import (
	"fmt"
	"strconv"
)

func main() {
	i, err := strconv.Atoi("42")
	if err != nil {
		fmt.Printf("couldn't convert number: %v\n", err)
		return
	}
	fmt.Println("Converted number:", i)
}
```

---

## Goroutines and Channels

### Goroutines

A **goroutine** is a lightweight thread managed by the Go runtime. You can launch a new goroutine with the `go` keyword.

### Example: Goroutine with Channel

```go
package main

import "fmt"

func main() {
	ch := make(chan int)
	go func() {
		ch <- 42
	}()
	fmt.Println(<-ch) // Outputs: 42
}
```

### Buffered Channels

Channels can be **buffered**, meaning they hold a specified number of items before blocking.

```go
package main

import "fmt"

func main() {
	ch := make(chan int, 2)
	ch <- 1
	ch <- 2

	// Receive and print values from the channel
	fmt.Println(<-ch) // Outputs: 1
	fmt.Println(<-ch) // Outputs: 2
}
```

If you try to send more data than the buffer can hold, it will cause a **deadlock**.

### Range and Close

You can **close** a channel to indicate that no more values will be sent. This is useful in range loops over channels.

```go
package main

import "fmt"

func main() {
	ch := make(chan int)
	go func() {
		for i := 0; i < 3; i++ {
			ch <- i
		}
		close(ch) // Close the channel
	}()
	
	for v := range ch {
		fmt.Println(v) // Outputs: 0, 1, 2
	}
}
```

---

## Select Statement

The `select` statement allows a goroutine to wait on multiple communication operations. It chooses one case at random if multiple channels are ready.

```go
package main

import "fmt"

func fibonacci(c, quit chan int) {
	x, y := 0, 1
	for {
		select {
		case c <- x:
			x, y = y, x + y
		case <-quit:
			fmt.Println("quit")
			return
		}
	}
}

func main() {
	c := make(chan int)
	quit := make(chan int)

	go func() {
		for i := 0; i < 10; i++ {
			fmt.Println(<-c)
		}
		quit <- 0
	}()

	fibonacci(c, quit)
}
```

---

## Mutex: Synchronizing Goroutines

If you want to ensure that only one goroutine accesses a shared resource at a time, you can use **mutexes**.

### Example: Using `sync.Mutex`

```go
package main

import (
	"fmt"
	"sync"
)

var counter int
var mu sync.Mutex // Declare a mutex

func increment() {
	mu.Lock()         // Lock the mutex before accessing the shared counter
	defer mu.Unlock() // Ensure the mutex is unlocked after the function finishes

	counter++ // Critical section - modify the counter
}

func main() {
	var wg sync.WaitGroup

	// Start 10 goroutines to increment the counter
	for i := 0; i < 10; i++ {
		wg.Add(1)
		go func() {
			defer wg.Done()
			increment()
		}()
	}

	// Wait for all goroutines to finish
	wg.Wait()

	// Print the final value of the counter
	fmt.Println("Final counter:", counter) // Outputs: 10
}
```

This ensures the counter is safely updated by each goroutine without race conditions.

---
