# Strategy

The strategy pattern is a behavioral design pattern that enables selecting an algorithm at runtime. It defines a family of algorithms, encapsulates each algorithm, and makes the algorithms interchangeable within that family.

The strategy pattern is particularly useful in Rust when you need to define a set of algorithms and choose one of them at runtime. It allows you to encapsulate the algorithm in a separate struct and switch between different algorithms without changing the client code.

## Implementation in Rust

In Rust, implementing the strategy pattern involves defining a trait that represents the strategy and implementing this trait for different concrete strategies. Here's an example to demonstrate how to implement the strategy pattern in Rust.

```rust
trait SortStrategy {
    fn sort(&self, data: &mut Vec<i32>);
}

struct BubbleSort;
impl SortStrategy for BubbleSort {
    fn sort(&self, data: &mut Vec<i32>) {
        for i in 0..data.len() {
            for j in 0..data.len() - 1 {
                if data[j] > data[j + 1] {
                    data.swap(j, j + 1);
                }
            }
        }
    }
}

struct QuickSort;

impl SortStrategy for QuickSort {
    fn sort(&self, data: &mut Vec<i32>) {
        if data.len() <= 1 {
            return;
        }

        let pivot = data.pop().unwrap();
        let mut left = Vec::new();
        let mut right = Vec::new();

        for x in data {
            if *x < pivot {
                left.push(*x);
            } else {
                right.push(*x);
            }
        }

        self.sort(&mut left);
        self.sort(&mut right);

        data.clear();
        data.extend(left);
        data.push(pivot);
        data.extend(right);
    }
}

struct Sorter {
    strategy: Box<dyn SortStrategy>,
}

impl Sorter {
    fn new(strategy: Box<dyn SortStrategy>) -> Self {
        Sorter { strategy }
    }

    fn sort(&self, data: &mut Vec<i32>) {
        self.strategy.sort(data);
    }
}

fn main() {
    let mut data = vec![3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5];
    let bubble_sort = Box::new(BubbleSort);
    let quick_sort = Box::new(QuickSort);

    let sorter = Sorter::new(bubble_sort);
    sorter.sort(&mut data);
    println!("Bubble sorted: {:?}", data);

    let sorter = Sorter::new(quick_sort);
    sorter.sort(&mut data);
    println!("Quick sorted: {:?}", data);
}
```
