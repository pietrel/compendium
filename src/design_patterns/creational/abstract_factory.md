# Abstract Factory

The Abstract Factory pattern is a creational design pattern that allows you to produce families of related objects without specifying their concrete classes. This pattern is particularly useful when a system needs to be independent of how its products are created, composed, and represented. It also provides a way to encapsulate a group of individual factories that have a common theme without specifying their concrete classes.

### Implementation in Rust

In Rust, implementing the Abstract Factory pattern involves using traits to define an interface for creating an abstract product and implementing this interface in different factories to create concrete products. Here’s a detailed example to demonstrate how to implement the Abstract Factory pattern in Rust.

```rust
trait Button {
    fn click(&self);
}

trait Checkbox {
    fn check(&self);
}

struct WinButton;
struct MacButton;

impl Button for WinButton {
    fn click(&self) {
        println!("Windows Button clicked");
    }
}

impl Button for MacButton {
    fn click(&self) {
        println!("Mac Button clicked");
    }
}

struct WinCheckbox;
struct MacCheckbox;

impl Checkbox for WinCheckbox {
    fn check(&self) {
        println!("Windows Checkbox checked");
    }
}

impl Checkbox for MacCheckbox {
    fn check(&self) {
        println!("Mac Checkbox checked");
    }
}

trait GUIFactory {
    fn create_button(&self) -> Box<dyn Button>;
    fn create_checkbox(&self) -> Box<dyn Checkbox>;
}

struct WinFactory;
struct MacFactory;

impl GUIFactory for WinFactory {
    fn create_button(&self) -> Box<dyn Button> {
        Box::new(WinButton)
    }

    fn create_checkbox(&self) -> Box<dyn Checkbox> {
        Box::new(WinCheckbox)
    }
}

impl GUIFactory for MacFactory {
    fn create_button(&self) -> Box<dyn Button> {
        Box::new(MacButton)
    }

    fn create_checkbox(&self) -> Box<dyn Checkbox> {
        Box::new(MacCheckbox)
    }
}

fn build_ui(factory: &dyn GUIFactory) {
    let button = factory.create_button();
    let checkbox = factory.create_checkbox();

    button.click();
    checkbox.check();
}

fn main() {
    let win_factory = WinFactory;
    let mac_factory = MacFactory;

    println!("Test UI with Windows Factory:");
    build_ui(&win_factory);

    println!("Test UI with Mac Factory:");
    build_ui(&mac_factory);
}
```





