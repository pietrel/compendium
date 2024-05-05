# Bubble Sort

Bubble Sort is a straightforward sorting algorithm that repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. The pass through the list is repeated until no swaps are needed, which means the list is sorted. Despite being easy to understand and implement, Bubble Sort is not very efficient for large datasets as its average and worst-case complexity is \\( O(n^2) \\).

## Implementation

### PHP

```php
function bubbleSort(array &$arr) {
    $n = count($arr);
    do {
        $swapped = false;
        for ($i = 1; $i < $n; $i++) {
            if ($arr[$i - 1] > $arr[$i]) {
                // Swap elements
                $temp = $arr[$i - 1];
                $arr[$i - 1] = $arr[$i];
                $arr[$i] = $temp;
                $swapped = true;
            }
        }
        $n--; // Decrement the count of items to be sorted
    } while ($swapped);
}

// Example usage
$arr = [64, 34, 25, 12, 22, 11, 90];
echo "Original array:\n";
print_r($arr);

bubbleSort($arr);
echo "Sorted array:\n";
print_r($arr);
```

### Go

```go
package main

import "fmt"

func bubbleSort(slice []int) {
    n := len(slice)
    for i := 0; i < n-1; i++ { // Outer loop for multiple passes
        swapped := false
        for j := 0; j < n-i-1; j++ { // Inner loop for each pass
            if slice[j] > slice[j+1] {
                // Swap elements if they are in the wrong order
                slice[j], slice[j+1] = slice[j+1], slice[j]
                swapped = true
            }
        }
        // If no elements were swapped, the slice is sorted
        if !swapped {
            break
        }
    }
}

func main() {
    slice := []int{64, 34, 25, 12, 22, 11, 90}
    fmt.Println("Original slice:", slice)
    bubbleSort(slice)
    fmt.Println("Sorted slice:", slice)
}
```

### Rust

Implementing Bubble Sort in Rust is simple. The following code snippet demonstrates how to sort an array of integers using Bubble Sort in Rust. The `bubble_sort` function takes a mutable reference to an array of integers and sorts it in place. The `main` function creates an array of integers, prints the original array, sorts it using Bubble Sort, and then prints the sorted array.

```rust
# use std::time::Instant;
#
fn bubble_sort(arr: &mut [i32]) {
    let mut n = arr.len();
    let mut swapped = true;

    while swapped {
        swapped = false;
        for i in 1..n {
            if arr[i - 1] > arr[i] {
                arr.swap(i - 1, i);
                swapped = true;
            }
        }
        n -= 1; 
    }
}
#
#fn sort_with_info(description: &str, arr: &mut [i32]){
    # let start = Instant::now();
    # println!("{}: {:?}", description, arr);
    # bubble_sort(arr);
    # println!("Sorted Result: {:?}", arr);
    # println!("Time elapsed is: {:?}", start.elapsed());
    # println!("");
#}
#
# fn main() {
    # let mut already_sorted_numbers = [11, 22, 25, 34, 64, 90];
    # sort_with_info("Already Sorted", &mut already_sorted_numbers);
    # let mut reverse_sorted_numbers = [90, 64, 34, 25, 22, 11];
    # sort_with_info("Reverse Sorted", &mut reverse_sorted_numbers);
    # let mut randomly_distributed_numbers = [64, 34, 25, 12, 22, 11, 90];
    # sort_with_info("Randomly Distributed", &mut randomly_distributed_numbers);
    # let mut nearly_sorted_numbers = [11, 25, 22, 34, 64, 90];
    # sort_with_info("Nearly Sorted", &mut nearly_sorted_numbers);
    # let mut few_unique_numbers = [34, 34, 34, 34, 34, 34];
    # sort_with_info("Few Unique", &mut few_unique_numbers);
# }
```

