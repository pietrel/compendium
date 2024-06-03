# Iterator

The Iterator pattern provides a way to access the elements of an aggregate object sequentially without exposing its underlying representation.

The Iterator pattern is used to provide a standard way to traverse a collection of items without exposing the underlying implementation. It allows you to access the elements of a collection sequentially without needing to know the internal structure of the collection.

```rust
trait Iterator {
    fn has_next(&self) -> bool;
    fn next(&mut self) -> Option<&str>;
}

struct ConcreteIterator {
    index: usize,
    data: Vec<String>,
}

impl ConcreteIterator {
    fn new(data: Vec<String>) -> Self {
        Self { index: 0, data }
    }
}

impl Iterator for ConcreteIterator {
    fn has_next(&self) -> bool {
        self.index < self.data.len()
    }

    fn next(&mut self) -> Option<&str> {
        if self.has_next() {
            let item = &self.data[self.index];
            self.index += 1;
            Some(item)
        } else {
            None
        }
    }
}

fn main() {
    let data = vec!["A".to_string(), "B".to_string(), "C".to_string()];
    let mut iterator = ConcreteIterator::new(data);

    while iterator.has_next() {
        if let Some(item) = iterator.next() {
            println!("{}", item);
        }
    }
}
```

```rust
struct Fibonnaci {
    current: u64,
    next: u64,
}

impl Iterator for Fibonnaci {
    type Item = u64;
    
    fn next (&mut self) -> Option<Self::Item> {
        let current = self.current;
        self.current = self.next;
        self.next = current + self.next;
        Some(current)
    }
}

fn fibonnaci() -> Fibonnaci {
    Fibonnaci { current: 0, next: 1 }
}

fn main() {
    let mut fib = fibonnaci();
    for i in 0..=10 {
        if let Some(n) = fib.next() {
            println!("{} -> {}", i, n);
        }
    }
}
```
