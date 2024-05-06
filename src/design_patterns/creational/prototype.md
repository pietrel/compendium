# Prototype

The Prototype pattern is a creational design pattern that allows cloning objects, even complex ones, without coupling to their specific classes. It is useful when the creation of an object is expensive or complex, and the object is similar to an existing object.

The Prototype pattern is particularly useful in Rust when you need to create objects that are similar to existing objects but have different configurations. It allows you to clone an existing object and modify its properties without creating a new object from scratch.

## Implementation in Rust

In Rust, implementing the Prototype pattern involves defining a struct that serves as the prototype and implementing the `Clone` trait for that struct. The `Clone` trait provides a `clone` method that creates a new object with the same properties as the original object. Here's an example to demonstrate how to implement the Prototype pattern in Rust.

```rust
#[derive(Clone)]
struct Circle {
    pub x: u32,
    pub y: u32,
    pub radius: u32,
}

fn main() {
    let circle1 = Circle {
        x: 10,
        y: 15,
        radius: 10,
    };

    // Prototype in action.
    let mut circle2 = circle1.clone();
    circle2.radius = 77;

    println!("Circle 1: {}, {}, {}", circle1.x, circle1.y, circle1.radius);
    println!("Circle 2: {}, {}, {}", circle2.x, circle2.y, circle2.radius);
}

```
