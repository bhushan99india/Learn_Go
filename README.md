# Learn_Go


### Reosources

Go Lang: Overview & download Link: https://golang.org/ 

```
Youtube Videos to start with: 
            Level 0:
                https://www.youtube.com/watch?v=JoJ8Sw5Yb4c&list=PLRAV69dS1uWQGDQoBYMZWKjzuhCaOnBpa&index=1
                https://www.linkedin.com/learning/go-essential-training
LinkedIn Videos to further ramp up: 
            Level 1:
                https://www.linkedin.com/learning/transition-from-java-to-go
                https://www.linkedin.com/learning/learning-the-go-standard-library

            level 2:
                https://www.linkedin.com/learning/practice-it-go-rest-api-server
                https://www.linkedin.com/learning/applied-concurrency-in-go

            Level 3:
                https://www.linkedin.com/learning/secure-coding-in-go![image](https://github.com/user-attachments/assets/2d406943-d26b-41bf-873f-164b7ab288fb)
```

### Interview question 
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

### Points to be remember in GO programing
1. Constants cannot be declared using the := syntax.
2. A switch statement is a shorter way to write a sequence of if - else statements.
3. Switch without a condition is the same as switch true.
4. Pointer zero value is nil
5. Unlike C, Go has no pointer arithmetic.(perform operations like incrementing or decrementing the pointer, or even adding/subtracting integers to shift the pointer to different locations in memory.)
6. A struct is a collection of fields.
7. An array's length is part of its type, so arrays cannot be resized
8. A slice, is a dynamically-sized, flexible view into the elements of an array.
9. Changing the elements of a slice modifies the corresponding elements of its underlying array.Other slices that share the same underlying array will see those changes.
10. The length of a slice is the number of elements it contains.
11. The capacity of a slice is the number of elements in the underlying array, counting from the first element in the slice.



