# Data Structures in Go

## Basic Data Structures

### Arrays

An array in Go is a fixed-length sequence of elements of a single type. Once an array is declared, it cannot be resized.
The length of an array is part of its type, so arrays cannot be resized.

```go
var a [3]int
a[0] = 1
a[1] = 2
a[2] = 3
```

### Slices

A slice is a variable-length sequence which is made up of elements of the same type. A slice is a reference to an
underlying array. A slice is a lightweight data structure that gives access to a section of an underlying array.

```go
var s []int
s = append(s, 1)
s = append(s, 2)
s = append(s, 3)
```

### Maps

A map is an unordered collection of key-value pairs. Maps are used to look up a value by its associated key.

```go
var m map[string]int
m = make(map[string]int)
m["foo"] = 1
m["bar"] = 2
```

### Structs

A struct is a composite data type that groups together variables of different types.

```go
type Person struct {
    Name string
    Age  int
}

p := Person{Name: "Alice", Age: 30}
```

## Advanced Data Structures

Go does not have a built-in implementation for advanced data structures like linked lists, stacks, queues, heaps, and
priority queues. However, these data structures can be implemented using slices and maps.

```go
type Stack struct {
    items []int
}

func (s *Stack) Push(item int) {
    s.items = append(s.items, item)
}

func (s *Stack) Pop() int {
    if len(s.items) == 0 {
        return -1
    }
    item := s.items[len(s.items)-1]
    s.items = s.items[:len(s.items)-1]
    return item
}
```go
