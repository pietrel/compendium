# Factory Method

Factory Method is a creational design pattern that provides an interface for creating objects in a superclass, but allows subclasses to alter the type of objects that will be created.

The Factory Method pattern is useful when you need to create an object that is part of a family of related objects. It allows you to create objects without specifying the exact class of object that will be created. This pattern is particularly useful when you need to create objects that share a common interface but have different implementations.

### Implementation in Rust

In Rust, implementing the Factory Method pattern involves defining a trait that serves as the factory interface and implementing this trait in different concrete factories to create specific objects. Here's an example to demonstrate how to implement the Factory Method pattern in Rust.

```rust
trait Vehicle {
    fn drive(&self);
}

struct Car;
impl Vehicle for Car {
    fn drive(&self) {
        println!("The car is driving.");
    }
}

struct Bike;
impl Vehicle for Bike {
    fn drive(&self) {
        println!("The bike is pedaling.");
    }
}

trait VehicleFactory {
    fn create_vehicle(&self) -> Box<dyn Vehicle>;
}

struct CarFactory;
impl VehicleFactory for CarFactory {
    fn create_vehicle(&self) -> Box<dyn Vehicle> {
        Box::new(Car)
    }
}

struct BikeFactory;
impl VehicleFactory for BikeFactory {
    fn create_vehicle(&self) -> Box<dyn Vehicle> {
        Box::new(Bike)
    }
}

fn main() {
    let car_factory = CarFactory;
    let bike_factory = BikeFactory;

    let car = car_factory.create_vehicle();
    let bike = bike_factory.create_vehicle();

    car.drive();
    bike.drive();
}
```
