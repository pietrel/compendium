# Bridge

The Bridge pattern is a structural design pattern that lets you split a large class or a set of closely related classes into two separate hierarchies—abstraction and implementation—which can be developed independently of each other.

```rust
trait Implementor {
    fn operation_implementation(&self) -> String;
}

struct ConcreteImplementorA;

impl Implementor for ConcreteImplementorA {
    fn operation_implementation(&self) -> String {
        String::from("ConcreteImplementorA: operation implementation")
    }
}

struct ConcreteImplementorB;

impl Implementor for ConcreteImplementorB {
    fn operation_implementation(&self) -> String {
        String::from("ConcreteImplementorB: operation implementation")
    }
}

trait Abstraction {
    fn operation(&self) -> String;
}

struct RefinedAbstraction {
    implementor: Box<dyn Implementor>,
}

impl Abstraction for RefinedAbstraction {
    fn operation(&self) -> String {
        format!("RefinedAbstraction: operation with {}", self.implementor.operation_implementation())
    }
}

fn client_code(abstraction: &dyn Abstraction) {
    println!("Client: I'm using the Abstraction interface: {}", abstraction.operation());
}

fn main() {
    let concrete_implementor_a = ConcreteImplementorA;
    let concrete_implementor_b = ConcreteImplementorB;

    let refined_abstraction = RefinedAbstraction {
        implementor: Box::new(concrete_implementor_a),
    };
    client_code(&refined_abstraction);

    let refined_abstraction = RefinedAbstraction {
        implementor: Box::new(concrete_implementor_b),
    };
    client_code(&refined_abstraction);
}
```
