# Proxy

The Proxy design pattern is a structural pattern that allows you to provide a substitute or placeholder for another object. This proxy manages access to the original object, enabling you to perform actions either before or after the request reaches the original object.

```rust
trait Subject {
    fn request(&self) -> String;
}

struct RealSubject;

impl Subject for RealSubject {
    fn request(&self) -> String {
        "RealSubject: Handling request".to_string()
    }
}

struct Proxy {
    real_subject: RealSubject,
}

impl Subject for Proxy {
    fn request(&self) -> String {
        "Proxy: Handling request".to_string()
    }
}

fn main() {
    let real_subject = RealSubject;
    let proxy = Proxy { real_subject };

    println!("{}", proxy.request());
}
```
