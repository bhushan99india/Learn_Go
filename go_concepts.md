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
```

This markdown file organizes the content into different sections, each addressing key concepts in Go, such as packages, type inference, loops, switch statements, defer, pointers, structs, and maps.

You can copy and paste this content into a `.md` file, and it will render as a properly formatted markdown document. Let me know if you need any changes!
