# Alignment and Padding

## Rust

Rust uses padding to ensure that each field in a struct is aligned to a memory address that is a multiple of its size.
This is done to optimize memory access and prevent performance penalties due to misaligned memory access.

Consider the following example:

```rust
#use std::mem;
#use std::time::{Duration, Instant};
#
// The #[repr(C)] attribute in Rust specifies the memory 
// layout of a struct to be compatible with C.
// Otherwise, the compiler is free to reorder fields 
// for better alignment and padding.

#[repr(C)] 
struct Suboptimal {
    a: u8,   // 1 byte
    b: u64,  // 8 bytes
    c: u16,  // 2 bytes
}

#[repr(C)]
struct Optimized {
    b: u64,  // 8 bytes
    c: u16,  // 2 bytes
    a: u8,   // 1 byte
}

#trait Initializable {
#    fn new(a: u8, b: u64, c: u16) -> Self;
#}
#
#impl Initializable for Suboptimal {
#    fn new(a: u8, b: u64, c: u16) -> Self {
#        Self { a, b, c }
#    }
#}
#
#impl Initializable for Optimized {
#    fn new(a: u8, b: u64, c: u16) -> Self {
#        Self { b, c, a }
#    }
#}
#
#trait Summable {
#    fn sum(&self) -> u64;
#}
#
#impl Summable for Suboptimal {
#    fn sum(&self) -> u64 {
#        self.a as u64 + self.b as u64 + self.c as u64
#    }
#}
#
#impl Summable for Optimized {
#    fn sum(&self) -> u64 {
#        self.a as u64 + self.b as u64 + self.c as u64
#    }
#}
#
const NUM_STRUCTS: usize = 1_000;

fn populate<T: Initializable>() -> (Vec<T>, Duration) {
#    let start = Instant::now();
    let data: Vec<T> = (0..NUM_STRUCTS)
        .map(|i| T::new((i % 256) as u8, i as u64, (i % 65536) as u16))
        .collect();
#    let population_time = start.elapsed();
#    (data, population_time)
}

#fn repeat_population<T: Initializable>(n: usize) -> Vec<Duration> {
#    (0..n)
#        .map(|_| {
#            let (_, duration) = populate::<T>();
#            duration
#        })
#        .collect()
#}
#
fn iterate_and_calculate<T: Summable>(data: &Vec<T>) -> (u64, Duration) {
#    let start = Instant::now();
    let total: u64 = data.iter().map(|s| s.sum()).sum();
#    let iteration_time = start.elapsed();
#    (total, iteration_time)
}

#fn repeat_iteration<T: Summable>(data: &Vec<T>, n: usize) -> (u64, Vec<Duration>) {
#    (0..n)
#        .map(|_| iterate_and_calculate(data))
#        .fold((0, Vec::new()), |(total, mut durations), (new_total, duration)| {
#            durations.push(duration);
#            (total + new_total, durations)
#        })
#}
#
fn main() {
#    println!("Optimized and Suboptimal Structs both hold 11 Bytes of data.");
#    println!("Size of Suboptimal Struct is {} bytes", mem::size_of::<Suboptimal>());
#    println!("Size of Optimized Struct is {} bytes", mem::size_of::<Optimized>());
#
    let n: usize = 3;

    let (sub_data, _) = populate::<Suboptimal>();
    let sub_population_time = repeat_population::<Suboptimal>(n);

    let (opt_data, _) = populate::<Optimized>();
    let opt_population_time = repeat_population::<Optimized>(n);

    let (_, sub_iteration_time) = repeat_iteration(&sub_data, n);
    let (_, opt_iteration_time) = repeat_iteration(&opt_data, n);
    
#    let (sub_total, _) = repeat_iteration(&sub_data, n);
#    let (opt_total, _) = repeat_iteration(&opt_data, n);
#
#    println!("Population Time:");
#    println!("  Suboptimal: {:?}", sub_population_time);
#    println!("  Optimized:  {:?}", opt_population_time);
#
#    println!("Iteration Time:");
#    println!("  Suboptimal: {:?}", sub_iteration_time);
#    println!("  Optimized:  {:?}", opt_iteration_time);
#
#    assert_eq!(sub_total, opt_total);
}
```

It is worth noting that the `Suboptimal` struct has a size of 24 bytes, while the `Optimized` struct has a size of 16
bytes. However, the memory layout of the `Optimized` struct is more efficient due to the alignment of the fields, which
can lead to better performance.

When running the code, you will observe that the `Optimized` struct has better performance in terms of population and
iteration times compared to the `Suboptimal` struct. This is due to the optimized memory layout of the `Optimized`
struct, which reduces the number of cache misses and improves memory access efficiency.

*Rust compiler provides the `#[repr(C)]` attribute to specify the memory layout of a struct to be compatible with C.
This can be useful when interfacing with C libraries or when you need to control the memory layout of a struct for
performance reasons. Without this attribute, the Rust compiler is free to reorder fields for better alignment and
padding, which may not be optimal for performance-critical applications.*