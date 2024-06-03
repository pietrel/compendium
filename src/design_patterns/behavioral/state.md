# State

The state pattern is a behavioral pattern that allows an object to change its behavior when its internal state changes.
The object will appear to change its class.

The state pattern is useful when an object's behavior is dependent on its state and it must change its behavior at runtime depending on that state.

### OOP like way 
Rust does not have a built-in state pattern, but it can be implemented using traits.

```rust
pub struct Post {
    state: Option<Box<dyn State>>,
    content: String,
}

impl Post {
    pub fn new() -> Post {
        Post {
            state: Some(Box::new(Draft {})),
            content: String::new(),
        }
    }

    // not part of state pattern
    pub fn add_text(&mut self, text: &str) {
        self.content.push_str(text);
    }

    pub fn content(&self) -> &str {
        self.state.as_ref().unwrap().content(&self)
    }

    pub fn request_review(&mut self) {
        if let Some(s) = self.state.take() {
            self.state = Some(s.request_review())
        }
    }

    pub fn approve(&mut self) {
        if let Some(s) = self.state.take() {
            self.state = Some(s.approve())
        }
    }
}

trait State {
    fn request_review(self: Box<Self>) -> Box<dyn State>;
    fn approve(self: Box<Self>) -> Box<dyn State>;
    fn content<'a>(&self, post: &'a Post) -> &'a str {
        ""
    }
}

struct Draft {}

impl State for Draft {
    fn request_review(self: Box<Self>) -> Box<dyn State> {
        Box::new(PendingReview {})
    }

    fn approve(self: Box<Self>) -> Box<dyn State> {
        self
    }
}

struct PendingReview {}

impl State for PendingReview {
    fn request_review(self: Box<Self>) -> Box<dyn State> {
        self
    }

    fn approve(self: Box<Self>) -> Box<dyn State> {
        Box::new(Published {})
    }
}

struct Published {}

impl State for Published {
    fn request_review(self: Box<Self>) -> Box<dyn State> {
        self
    }

    fn approve(self: Box<Self>) -> Box<dyn State> {
        self
    }

    fn content<'a>(&self, post: &'a Post) -> &'a str {
        &post.content
    }
}

fn main() {
    let mut post = Post::new();
    
    post.add_text("I ate a salad for lunch today");
    assert_eq!("", post.content());
    
    post.request_review();
    assert_eq!("", post.content());
    
    post.approve();
    assert_eq!("I ate a salad for lunch today", post.content());
    
    println!("{}", post.content());
}

```

### Functional way

We utilize Rust ownership system to enforce the state transitions.

```rust

struct Post {
    content: String,
}

impl Post {
    fn new() -> DraftPost {
        DraftPost {
            content: String::new(),
        }
    }
    
    fn content(&self) -> &str {
        &self.content
    }
}


struct DraftPost {
    content: String,
}


impl DraftPost {
    fn add_text(&mut self, text: &str) {
        self.content.push_str(text);
    }
    
    fn request_review(self) -> PendingReviewPost {
        PendingReviewPost {
            content: self.content,
        }
    }
}

struct PendingReviewPost {
    content: String,
}

impl PendingReviewPost {
    fn approve(self) -> Post {
        Post {
            content: self.content,
        }
    }
}

fn main() {
    let mut post: DraftPost = Post::new();
    
    post.add_text("I ate a salad for lunch today");
    
    let post: PendingReviewPost = post.request_review();
    
    let post: Post = post.approve();
    assert_eq!("I ate a salad for lunch today", post.content());
    
    println!("{}", post.content());
}


```
