# Builder

The Builder pattern is a creational design pattern used to construct complex objects step by step. It allows you to produce different types and representations of an object using the same construction code. This pattern is particularly useful in Rust when you need to build objects that have several optional or configurable properties.

### Implementation in Rust

In Rust, implementing the Builder pattern involves defining a builder struct that is responsible for constructing the object. The builder struct contains methods to set the optional properties of the object and a build method to create the final object. Here's an example to demonstrate how to implement the Builder pattern in Rust.

```rust
struct Car {
    make: String,
    model: String,
    color: Option<String>,
    transmission: Option<String>,
    convertible: Option<bool>,
}
struct CarBuilder {
    make: String,
    model: String,
    color: Option<String>,
    transmission: Option<String>,
    convertible: Option<bool>,
}

impl CarBuilder {
    // Constructor to start the building process
    fn new(make: &str, model: &str) -> Self {
        CarBuilder {
            make: make.to_string(),
            model: model.to_string(),
            color: None,
            transmission: None,
            convertible: None,
        }
    }

    // Method to set the color of the car
    fn color(mut self, color: &str) -> Self {
        self.color = Some(color.to_string());
        self
    }

    // Method to set the transmission type
    fn transmission(mut self, transmission: &str) -> Self {
        self.transmission = Some(transmission.to_string());
        self
    }

    // Method to specify if it is a convertible
    fn convertible(mut self, convertible: bool) -> Self {
        self.convertible = Some(convertible);
        self
    }

    // Final method to build the Car
    fn build(self) -> Car {
        Car {
            make: self.make,
            model: self.model,
            color: self.color,
            transmission: self.transmission,
            convertible: self.convertible,
        }
    }
}

fn main() {
    let car = CarBuilder::new("Toyota", "Corolla")
        .color("red")
        .transmission("manual")
        .convertible(true)
        .build();

    println!("Car Make: {}", car.make);
    println!("Car Model: {}", car.model);
    println!("Car Color: {:?}", car.color);
    println!("Car Transmission: {:?}", car.transmission);
    println!("Car Convertible: {:?}", car.convertible);
}

```
