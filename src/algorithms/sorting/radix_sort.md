# Radix Sort

Radix Sort is a non-comparative integer sorting algorithm that sorts data with integer keys by grouping keys by individual digits that share the same significant position and value. It is a linear time complexity sorting algorithm that is efficient for sorting large numbers of integers. Radix Sort is often used to sort numbers in a fixed range, such as integers with a fixed number of digits.


```rust
# use std::time::Instant;
#
fn radix_sort(arr: &mut [i32]) {
    // Here we define the radix of the number system, which is 10 for decimal numbers
    let radix = 10;  
    let mut done = false;
    // Starting with the least significant digit
    let mut digit_position = 1;  

    while !done {
        // Assume the loop is done unless we find an element with a higher place value
        done = true;  
        // Create buckets for each digit from 0 to 9
        let mut buckets: Vec<Vec<i32>> = vec![vec![]; radix as usize];  

        // Place each number in the corresponding bucket based on its current digit
        for &number in arr.iter() {
            let digit = (number / digit_position) % radix;
            buckets[digit as usize].push(number);
            if done && digit > 0 {  
            // Check if there are still numbers with more digits left to process
                done = false;
            }
        }

        // Collect numbers back from buckets to array
        let mut idx = 0;
        for bucket in &buckets {
            for &number in bucket {
                arr[idx] = number;
                idx += 1;
            }
        }

        // Move to the next more significant digit
        digit_position *= radix;  
    }
}
#
#fn sort_with_info(description: &str, arr: &mut [i32]){
    # let start = Instant::now();
    # println!("{}: {:?}", description, arr);
    # radix_sort(arr);
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
