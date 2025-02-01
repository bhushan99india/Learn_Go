# Learn_Go

### Go Learning Resources

### [Click Here](GO//resources.md) to view all Go Learning Resources.

# Go Programming Concepts

### [Click Here](/go_concepts.md) to view all Programming Concepts in go.

# Go Interview question

### [Click Here](GO/interview_questions.md) to view all Interview question in go.

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
12. channel, close channel
13. wait groups
14. buffered channel:- need to wait  for receiver
15. we can you range on unbuffered channel also. but channel closing is important to avoid panic
16. if channel is already close and try to range, nothing will happened.
17. len and cap function works on channel
18. select keyword used when you have multiple channel and you want to get data from who is come first.
19. infinite for loop and select can be use together where continuously data coming in multiple goroutines
20. GOTO allows for an unconditional jump to another part of the program, typically to a labeled statement
21. single character (e.g., 'b') to its ASCII value (which is an integer), you need to work with a rune (which is Go's representation for Unicode characters) rather than a string.
22. In Go, single quotes are for characters (a rune), and double quotes are for strings.





