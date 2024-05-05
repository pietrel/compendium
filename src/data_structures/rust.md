# Data Structures in Rust

## Arrays

An array in Rust is a fixed-size sequence of elements of the same type. Once an array is declared, it cannot be resized. The length of an array is part of its type, so arrays cannot be resized. 

```rust, noplayground
let a = [1, 2, 3];
```

## Vectors

A vector is a variable-length sequence which is made up of elements of the same type. A vector is a reference to an underlying array. A vector is a growable data structure that gives access to a section of an underlying array. 

```rust, noplayground
let mut v = vec![1, 2, 3];
v.push(4);
v.push(5);
```

## Slices

A slice is a reference to a contiguous sequence of elements in a collection. Slices are used to give a reference to a section of an array or a vector. 

```rust, noplayground
let a = [1, 2, 3, 4, 5];
let slice = &a[1..3];
```

## Hash Maps

A hash map is a collection of key-value pairs. Hash maps are used to look up a value by its associated key. 

```rust, noplayground
use std::collections::HashMap;

let mut scores = HashMap::new();

scores.insert(String::from("Blue"), 10);
scores.insert(String::from("Yellow"), 50);
```

## Enums

An enum is a type that can have a fixed set of values. Each value is called a variant. Enums are useful for representing a small, fixed set of related values. 

```rust, noplayground
enum IpAddr {
    V4(u8, u8, u8, u8),
    V6(String),
}

let home = IpAddr::V4(127, 0, 0, 1);
let loopback = IpAddr::V6(String::from("::1"));
```

## Advanced Data Structures

### Structs

Structs in Rust are used to create custom data types by combining multiple other types. Structs are crucial for practical Rust programming, allowing you to encapsulate related data into one cohesive unit.

```rust
struct Person {
    name: String,
    age: u8,
}
impl Person {
    fn greet(&self) {
        println!("Hello, my name is {} and I am {} years old.", self.name, self.age);
    }
}

let p = Person {
    name: String::from("Alice"),
    age: 30,
};
p.greet();
```

### Linked Lists

Rust's standard library provides two types of linked lists: `LinkedList` and `VecDeque`. `LinkedList` is a doubly-linked list, which allows efficient insertion and removal of elements from both ends of the list.

```rust
use std::collections::LinkedList;

let mut list: LinkedList<u32> = LinkedList::new();
list.push_back(1);
list.push_back(2);
list.push_front(0);
println!("{:?}", list); // Outputs: [0, 1, 2]
```


### Stacks

A stack is a last in, first out (LIFO) data structure. In Rust, you can implement a stack using a `Vec` and push and pop elements from the end of the vector.

```rust
struct Stack {
    items: Vec<i32>,
}

impl Stack {
    fn push(&mut self, item: i32) {
        self.items.push(item);
    }

    fn pop(&mut self) -> Option<i32> {
        self.items.pop()
    }
}

fn main() {
    let mut stack = Stack { items: vec![] };
    stack.push(1);
    stack.push(2);
    stack.push(3);

    while let Some(item) = stack.pop() {
        println!("{}", item);
    }
}
```
