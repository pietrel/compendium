# Extension traits

Extension traits are a way to extend the functionality of a type without modifying the original type. This is useful when you want to add methods to a type that you don't own, such as types from external libraries or the standard library.

Extension traits are implemented using the `trait` keyword followed by the name of the trait and the type that you want to extend. The methods defined in the extension trait can be called on any instance of the type that implements the trait.

```rust
trait Palindrome {
    fn is_palindrome(&self) -> bool;
}

impl Palindrome for String {
    fn is_palindrome(&self) -> bool {
        let s = self.chars().collect::<Vec<char>>();
        s == s.iter().rev().cloned().collect::<Vec<char>>()
    }
}

fn main() {
    let mut x = String::from("racecar");
    println!("{}", x.is_palindrome());
    x = String::from("hello");
    println!("{}", x.is_palindrome());
}
```
