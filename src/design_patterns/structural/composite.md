# Composite

The Composite pattern is a structural design pattern that lets you compose objects into tree structures to represent part-whole hierarchies. Composite lets clients treat individual objects and compositions of objects uniformly.

```rust
trait Component {
    fn operation(&self) -> String;
}

struct Leaf {
    name: String,
}

impl Component for Leaf {
    fn operation(&self) -> String {
        format!("Leaf: {}", self.name)
    }
}

struct Composite {
    children: Vec<Box<dyn Component>>,
}

impl Component for Composite {
    fn operation(&self) -> String {
        let mut result = String::new();
        for child in &self.children {
            if !result.is_empty() {
                result.push_str(", ");
            }
            result.push_str(&child.operation());
        }
        format!("Branch: [{}]", result)
    }
}

fn client_code(component: &dyn Component) {
    println!("Client: I got a composite component:");
    println!("RESULT: {}", component.operation());
}

fn main() {
    let leaf = Leaf {
        name: String::from("Leaf"),
    };
    client_code(&leaf);

    let composite = Composite {
        children: vec![
            Box::new(Leaf {
                name: String::from("Leaf A"),
            }),
            Box::new(Leaf {
                name: String::from("Leaf B"),
            }),
        ],
    };
    client_code(&composite);
}
```
