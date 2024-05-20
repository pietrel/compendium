# Newtype

Newtype is a design pattern that allows you to create a new type that is distinct from its original type. This pattern is useful when you want to add some additional functionality to an existing type without creating a new type from scratch.

```rust
use std::fmt::Display;

// Create Newtype Password to override the Display trait for String
struct Password(String);

impl Display for Password {
    fn fmt(&self, f: &mut std::fmt::Formatter<'_>) -> std::fmt::Result {
        write!(f, "****************")
    }
}

fn main() {
    let unsecured_password: String = "ThisIsMyPassword".to_string();
    let secured_password: Password = Password(unsecured_password.clone());
    println!("unsecured_password: {unsecured_password}");
    println!("secured_password: {secured_password}");
}
```

## Advantages

- Allows you to create a new type that is distinct from its original type.
- Provides a way to add additional functionality to an existing type without creating a new type from scratch.
- Helps in type safety by preventing accidental misuse of the original type.
- Improves code readability by giving a descriptive name to the new type.
- Enables you to implement traits for the new type without affecting the original type.

## Disadvantages

- Requires additional boilerplate code to define the newtype and implement traits for it.
- May lead to code duplication if the newtype needs to implement the same traits as the original type.
- Can introduce confusion if the newtype is not used consistently throughout the codebase.

## When to Use

- When you want to create a new type that is distinct from its original type.
- When you need to add additional functionality to an existing type without modifying the original type.
- When you want to improve type safety by preventing accidental misuse of the original type.
- When you need to implement traits for a specific use case without affecting the original type.

## Example Use Cases

- Creating a new type to represent a secure version of an existing type (e.g., Password).
- Wrapping a primitive type to provide additional validation or formatting (e.g., Email, PhoneNumber).
- Defining a new type to represent a specific domain concept (e.g., UserId, ProductId).
- Implementing traits for a specific use case without affecting the original type (e.g., Display, Debug).
