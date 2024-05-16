# Decorator

The Decorator pattern is a structural design pattern that allows adding new behaviors to objects dynamically by placing them inside special wrapper objects that contain these behaviors.

```rust
trait Component {
    fn operation(&self) -> String;
}

struct ConcreteComponent;

impl Component for ConcreteComponent {
    fn operation(&self) -> String {
        "ConcreteComponent".to_string()
    }
}

struct Decorator {
    component: Box<dyn Component>,
}

impl Decorator {
    fn new(component: Box<dyn Component>) -> Self {
        Self { component }
    }
}

impl Component for Decorator {
    fn operation(&self) -> String {
        format!("Decorator({})", self.component.operation())
    }
}

fn main() {
    let component = Box::new(ConcreteComponent);
    let decorator = Decorator::new(component);
    println!("{}", decorator.operation());
}
```

```php
<?php

interface Component
{
    public function operation(): string;
}

class ConcreteComponent implements Component
{
    public function operation(): string
    {
        return "ConcreteComponent";
    }
}

class Decorator implements Component
{
    private Component $component;

    public function __construct(Component $component)
    {
        $this->component = $component;
    }

    public function operation(): string
    {
        return "Decorator(" . $this->component->operation() . ")";
    }
}

$component = new ConcreteComponent();

$decorator = new Decorator($component);

echo $decorator->operation();
```

```go
package main

import "fmt"

type Component interface {
    Operation() string
}

type ConcreteComponent struct{}

func (c *ConcreteComponent) Operation() string {
    return "ConcreteComponent"
}

type Decorator struct {
    component Component
}

func (d *Decorator) Operation() string {
    return fmt.Sprintf("Decorator(%s)", d.component.Operation())
}

func NewDecorator(component Component) *Decorator {
    return &Decorator{component: component}
}

func main() {
    component := &ConcreteComponent{}
    decorator := NewDecorator(component)
    fmt.Println(decorator.Operation())
}
```
