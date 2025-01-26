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
 **Question 1: Difference between array and slice**

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



