# Quick Sort


```rust
# use std::time::Instant;
#
fn quicksort(arr: &mut [i32]) {
    // Base case: arrays with less than 2 elements are already sorted
    if arr.len() <= 1 {
        return;
    }

    // Partitioning phase
    let pivot_index = partition(arr);

    // Recursively apply the same logic to the left and right subarrays
    quicksort(&mut arr[0..pivot_index]);
    quicksort(&mut arr[pivot_index + 1..]);
}

fn partition(arr: &mut [i32]) -> usize {
    let pivot = arr[arr.len() - 1];  // Using the last element as the pivot
    let mut i = 0;

    for j in 0..arr.len() - 1 {
        if arr[j] <= pivot {
            arr.swap(i, j);
            i += 1;
        }
    }

    // Swap the pivot element to its correct position
    arr.swap(i, arr.len() - 1);
    i  // Return the index of the pivot element
}
#
#fn sort_with_info(description: &str, arr: &mut [i32]){
    # let start = Instant::now();
    # println!("{}: {:?}", description, arr);
    # quicksort(arr);
    # println!("Sorted Result: {:?}", arr);
    # println!("Time elapsed is: {:?}", start.elapsed());
    # println!("");
#}
#
# fn main() {
# let mut sorted = vec![11, 22, 25, 34, 64, 90];
    # sort_with_info("Already Sorted", &mut sorted);
    #
    # let mut reverse_sorted = vec![90, 64, 34, 25, 22, 11];
    # sort_with_info("Reverse Sorted", &mut reverse_sorted);
    # 
    # // Randomly distributed array
    # let mut random = vec![64, 34, 25, 12, 22, 11, 90];
    # sort_with_info("Randomly Distributed", &mut random);
    # 
    # // Nearly sorted array
    # let mut nearly_sorted = vec![11, 25, 22, 34, 64, 90];
    # sort_with_info("Nearly Sorted", &mut nearly_sorted);
    # 
    # // Few unique elements
    # let mut few_unique = vec![34, 34, 34, 34, 34, 34];
    # sort_with_info("Few Unique", &mut few_unique);
# }
```
