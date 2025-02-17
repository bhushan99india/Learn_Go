### Interview Questions
### **Question 1: Difference between array and slice**

| **Feature**                | **Array**                                                         | **Slice**                                                                                   |
|----------------------------|-------------------------------------------------------------------|---------------------------------------------------------------------------------------------|
| **Declaration**             | `var arr [5]int`<br>`arr := [3]int{1, 2, 3}`                      | `var s []int`<br>`s := []int{1, 2, 3}`                                                      |
| **Description**             | Fixed size array.                                                 | Slices are like references to arrays. A slice does not store any data, it just describes a section of an underlying array. |
| **Size**                    | Fixed at compile time. Cannot change.                             | Dynamic. Can grow or shrink using `append`.                                                 |
| **Type**                    | `[N]T` (e.g., `[5]int`, `[3]string`)                               | `[]T` (e.g., `[]int`, `[]string`)                                                           |
| **Memory Storage**          | All elements stored contiguously in memory.                       | A slice is a descriptor containing: <br> 1. A pointer to an underlying array <br> 2. Length <br> 3. Capacity. |
| **Passing to Functions**    | Passed by value (a copy of the array is made).<br> Pass by pointer for modification. | Passed by reference (internally, a pointer to the underlying array is passed).             |
| **Modification**            | Changes to a copied array do not affect the original.             | Changes to a slice's elements affect the underlying array.                                  |
| **Resizing**                | Not possible. Fixed size.                                         | Possible with `append`. Capacity may increase automatically.                                |
| **Underlying Data**         | Does not rely on other structures.                                | Built on top of an array; shares memory with it.                                            |
| **Projection**              | Not applicable.                                                   | Can create subslices sharing the same underlying array.                                    |
| **Example of Resizing**     | Not applicable.                                                   | `s := []int{1, 2, 3}`<br>`s = append(s, 4, 5)`                                              |
| **Performance**             | Faster due to no overhead for resizing or tracking capacity.      | Slight overhead for dynamic resizing and capacity tracking.                                |
| **Usage with Ranges**       | Requires manual bounds checking in loops.                         | Supports easy slicing: `s := arr[1:4]`.                                                     |
| **When to Use**             | For fixed-size collections. Rarely used in Go.                    | Preferred for most use cases due to flexibility and dynamic nature.                         |
| **Preferred Use**           | Low-level memory manipulation or specific fixed-size needs (e.g., matrix operations). | Common for dynamic collections like lists or arrays in most Go programs.                    |
| **Nil slices**              | Not applicable.                                                   | The zero value of a slice is `nil`. A nil slice has a length and capacity of 0 and has no underlying array. |

### **Question: 2 Differentiation Between Length and Capacity in Go Slices**

| **Property**    | **Length**                                                                                                                                   | **Capacity**                                                                                                                                                                                   |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Definition**  | The **length** of a slice is the number of elements it currently holds. **Example**: For `s := []int{1, 2, 3}`, `len(s)` is `3`.            | The **capacity** of a slice is the total number of elements that the slice can accommodate in the underlying array before a new allocation is needed. **Example**: For `s := []int{1, 2, 3}`, `cap(s)` could be `3` (depending on the internal array size). |
| **Example**     | `s := []int{1, 2, 3}`<br> `fmt.Println(len(s))` prints `3`.                                                                                 | `s := []int{1, 2, 3}`<br> `fmt.Println(cap(s))` prints `3` or more depending on Go's internal capacity allocation.                                                                             |
| **Nature**      | **Dynamic**: The **length** can change as elements are added or removed. **Example**: After appending elements, `len(s)` increases.          | **Static** initially, but can grow as necessary when elements are appended. **Example**: If `cap(s)` is 3 and you append more elements, Go will reallocate and increase the capacity automatically.  |
| **Example**     | ```go<br>s := []int{1, 2, 3}<br>s = append(s, 4, 5)<br>fmt.Println(len(s))  // Output: 5```                                                        | ```go<br>s := []int{1, 2, 3}<br>s = append(s, 4, 5)<br>fmt.Println(cap(s))  // Output: 6 (or more)```                                                                                           |
| **Impact of `append`** | **Length** increases as new elements are added with `append()`. **Example**: After appending, `len(s)` increases.                        | **Capacity** may increase automatically if the current capacity is exceeded. **Example**: If `cap(s)` was `3` and you append more than that, Go may increase the capacity, such as to `6`. |
| **Example**     | ```go<br>s := []int{1, 2, 3}<br>s = append(s, 4, 5)<br>fmt.Println(len(s))  // Output: 5```                                                        | ```go<br>s := []int{1, 2, 3}<br>s = append(s, 4, 5)<br>fmt.Println(cap(s))  // Output: 6 (capacity increases)```                                                                                 |
| **Memory Efficiency** | **Length** represents the **actual** number of elements being used in the slice. **Example**: `len(s)` will give the count of elements. | **Capacity** indicates how much memory is allocated to store elements. A larger capacity may be pre-allocated for potential growth. **Example**: If `cap(s)` is 10, more space is allocated than `len(s)`. |
| **Example**     | `s := []int{1, 2, 3}`<br> `fmt.Println(len(s))` prints `3`                                                                                   | `s := []int{1, 2, 3}`<br> `fmt.Println(cap(s))` might print `10` if Go allocated extra capacity.                                                                                                  |
| **Re-slicing**  | When you re-slice, the **length** changes based on the new slice boundaries. **Example**: `len(s[1:])` gives `5` for a slice with 6 elements. | **Capacity** of the slice remains unchanged unless you append and exceed the current capacity. **Example**: Re-slicing does not change capacity unless the new slice exceeds the capacity, and Go reallocates. |
| **Example**     | ```go<br>s := []int{1, 2, 3, 4, 5, 6}<br>s = s[1:]<br>fmt.Println(len(s))  // Output: 5```                                                        | ```go<br>s := []int{1, 2, 3, 4, 5, 6}<br>s = s[1:]<br>fmt.Println(cap(s))  // Output: 6 (unchanged unless new append exceeds capacity)```                                                       |
| **Nil Slices**  | A **nil slice** has **length 0**. **Example**: `len(s)` is `0` if `s` is nil.                                                                 | A **nil slice** has **capacity 0**. **Example**: `cap(s)` is `0` if `s` is nil. However, you can create a slice with length `0` but non-zero capacity using `make([]int, 0, 5)`. |
| **Example**     | `var s []int`<br> `fmt.Println(len(s))` prints `0`                                                                                             | `var s []int`<br> `fmt.Println(cap(s))` prints `0`<br> `s = make([]int, 0, 5)`<br> `fmt.Println(cap(s))` prints `5`                                                                                 |

---

### **Detailed Example of Length and Capacity in Action:**

```go
package main

import "fmt"

func main() {
	// Initial slice
	s := []int{1, 2, 3}
	fmt.Println("Initial slice:")
	fmt.Printf("len=%d cap=%d %v\n", len(s), cap(s), s)

	// Append more elements
	s = append(s, 4, 5, 6)
	fmt.Println("\nAfter appending elements:")
	fmt.Printf("len=%d cap=%d %v\n", len(s), cap(s), s)

	s = s[:0]
	fmt.Println("\nSlice the slice to give it zero length:")
	fmt.Printf("len=%d cap=%d %v\n", len(s), cap(s), s)

	// Re-slice
	//	s = s[2:]
	//panic: runtime error: slice bounds out of range [2:0]
	// s = s[:10]

	// Re-slice
	s = s[2:5]
	fmt.Println("\nAfter re-slicing:")
	fmt.Printf("len=%d cap=%d %v\n", len(s), cap(s), s)

	//panic: runtime error: slice bounds out of range [:6] with capacity 4
	// s = s[:6]

	// get extra element from array
	s = s[:4]
	fmt.Println("\nget extra element from array")
	fmt.Printf("len=%d cap=%d %v\n", len(s), cap(s), s)

	// Drop its first two values.
	s = s[2:]
	fmt.Println("\nDrop its first two values")
	fmt.Printf("len=%d cap=%d %v\n", len(s), cap(s), s)

	// Nil slice
	var t []int
	fmt.Println("\nNil slice:")
	fmt.Printf("len(t) = %d, cap(t) = %d\n", len(t), cap(t))

	// Create a slice with length 0 and capacity 5
	t = make([]int, 0, 5)
	fmt.Println("\nZero-length slice with capacity:")
	fmt.Printf("len(t) = %d, cap(t) = %d\n", len(t), cap(t))
}

```

### Output:
```text
Initial slice:
len=3 cap=3 [1 2 3]

After appending elements:
len=6 cap=6 [1 2 3 4 5 6]

Slice the slice to give it zero length:
len=0 cap=6 []

After re-slicing:
len=3 cap=4 [3 4 5]

get extra element from array
len=4 cap=4 [3 4 5 6]

Drop its first two values
len=2 cap=2 [5 6]

Nil slice:
len(t) = 0, cap(t) = 0

Zero-length slice with capacity:
len(t) = 0, cap(t) = 5
```

---

### **Summary of Key Points:**

- **Length** represents the **current number of elements** in the slice.
- **Capacity** refers to the **allocated size** in memory, determining how much space is reserved for potential growth.
- **Re-slicing** adjusts the slice's **length**, but **capacity** stays the same unless `append()` increases it.
- **Nil slices** have a **length of 0** and **capacity of 0**.
- **Appending** elements can increase **capacity** if needed.
- **Slice Base Changes:** When slicing, the "base" of the slice is adjusted relative to the underlying array. Further slicing operations use this new base.

```
map internal implementation

TTL Cache 

memory model golang

exit go routine

channel close

CAP theorem

cap theorem cassandra vs mongodb

https://www.instaclustr.com/blog/cassandra-vs-mongodb/

consistant hashing

service discovery

authorization

JWT parsing

dockerfile, dockercompose

2 phase commit

Saga Pattern

Microservices Saga Pattern

https://www.baeldung.com/cs/saga-pattern-microservices

Fargate Components Task Defination
Memory cpu  container env command client access via IP addressa and port,
incase  if any task crash , a new node is going to get spawned 
This is solved by Service will never go off and never change ip 
create task then create service for client ot connect to client >> service >> task



Layers of OSI model
http vs https
Datatypes in Golang
Interface in golang and its use
consurrency vs parallelism
goroutine vs thread (java/os) 
channels buffer, unbuffer
slice vs array >> cap, len >> append , slice is passed as parameter and then append
closure
size of int >> depends on architecture / platform 
runtime package
gomaxprocs(number of core)
gopath and goroot
find type of variable >> 3 ways fmt.Printf("%T",var) , fmt.Println(reflect.TypeOf(var1) , reflect.ValueOf(var1).Kind())
m:=make(map[string]interface{})
rune vs string
""
''
``
singleton design pattern
if 2 structs are given compare them >> reflect.DeepEqual() 
compiletime and runtime in golang
why are goroutines lightweight stackspace is 2kb(variable) >> 2000kb  , OS thread stackspace is 2MB 2000MB
defer/ recover/panic

sync package waitgroup, mutex read, write on in memory data lock unlock
init
unit testcase go mock mockgen tool
garbage collection  algorithm (tri color mark sweep algo),go memory model
how go code compiles static binding

even odd print using go routine alternate
channels with select with default
internal implementation of MAP in golang 
implement queue and stack and linked list in golang
write rest api using gorilla mux
2 phase commit, both  saga pattern , circuit breaker service discovery

image >> aws ecr >> aws ecs >> task defination  and the task defination autoscale autoscaling in aws 
API gateway, zookeeper, loadbalancer , kafka 
every 1 minute send mem and cpu usage data to cloudwatch , autoscaling >>> 3 strategy >> alarms
cloudwatch keeps logs of containers

expose container on internet how to do it >> public subnet internetgateway, private subnet and  NAT gateway,
DNS resolution service discovery
SOLID principle
Dependency Injection in Golang

```

