# Object Pool

Object Pool is a creational design pattern that provides a pool of objects that clients can reuse and recycle. It is useful when the cost of creating an object is high, and the number of objects in use is high.

Object Pool maintains a pool of reusable objects and manages the creation, destruction, and reuse of these objects. When a client requests an object, the Object Pool checks if there are any available objects in the pool. If an object is available, it is returned to the client; otherwise, a new object is created and added to the pool.

Object Pool can improve performance by reducing the overhead of creating and destroying objects. It can also help in managing limited resources efficiently by recycling objects instead of creating new ones.

### Example Implementation in Rust

```rust
use std::sync::{Arc, Mutex};
use std::collections::VecDeque;

struct PoolObject {
    id: usize, // Example property
}

struct ObjectPool {
    available: Mutex<VecDeque<Arc<PoolObject>>>,
}

impl ObjectPool {
    // Initialize the ObjectPool with a given number of pre-allocated objects
    fn new(size: usize) -> ObjectPool {
        let mut objects = VecDeque::with_capacity(size);
        for i in 0..size {
            objects.push_back(Arc::new(PoolObject { id: i }));
        }
        ObjectPool {
            available: Mutex::new(objects),
        }
    }

    // Retrieve an object from the pool
    fn get(&self) -> Option<Arc<PoolObject>> {
        let mut pool = self.available.lock().unwrap();
        pool.pop_front()
    }

    // Return an object to the pool
    fn put(&self, item: Arc<PoolObject>) {
        let mut pool = self.available.lock().unwrap();
        pool.push_back(item);
    }
}

fn main() {
    let pool = ObjectPool::new(2); // Create a pool with 2 objects

    // Get an object from the pool
    let object1 = pool.get().expect("No objects available");
    println!("Got object with ID: {}", object1.id);

    // Get another object
    let object2 = pool.get().expect("No objects available");
    println!("Got object with ID: {}", object2.id);

    // Return objects to the pool
    pool.put(object1);
    pool.put(object2);

    // Retrieve an object again to demonstrate reuse
    let object3 = pool.get().expect("No objects available");
    println!("Got object with ID: {}", object3.id);
}
```
