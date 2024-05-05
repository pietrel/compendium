# Data Structures in PHP

## Basic Data Structures

### Arrays

An array in PHP is an ordered map (PHP arrays are in fact implemented as ordered hashtables). It can be used as an array, list, hash table, dictionary, collection, stack and queue.

```php
$array = ["foo", "bar", "baz"];

$array = [
    "foo" => "bar",
    "bar" => "foo",
];
```

### Objects

Objects in PHP are created by instantiating a class. An object is an instance of a class. A class is a blueprint for an object.

```php
class Foo {
    public $foo;
    public $bar;

    public function __construct($foo, $bar) {
        $this->foo = $foo;
        $this->bar = $bar;
    }
    
    public function getFoo() {
        return $this->foo;
    }    
}
```

### Enumerations

With the release of PHP 8.1, PHP introduced built-in support for enumerations, commonly known as enums. Enums are a way to define a type that can have a fixed set of values. Prior to PHP 8.1, developers often used class constants to achieve similar functionality, but native enum support offers a more robust, integrated, and semantic approach.

#### Basic Enum

```php
enum Status {
    case Pending;
    case Approved;
    case Denied;
}

function printStatus(Status $status) {
    echo $status->name;
}

printStatus(Status::Pending); // Outputs: Pending
```

#### Enum with Values

```php
enum Status: string {
    case Pending = 'p';
    case Approved = 'a';
    case Denied = 'd';
}

function printStatus(Status $status) {
    echo $status->value;
}

printStatus(Status::Pending); // Outputs: p
```

## Advanced Data Structures

Standard PHP Library (SPL) has introduced a number of data structures that are available in PHP. These include:
- [SplDoublyLinkedList](https://www.php.net/manual/en/class.spldoublylinkedlist.php)
  - [SplStack](https://www.php.net/manual/en/class.splstack.php)
  - [SplQueue](https://www.php.net/manual/en/class.splqueue.php)
- [SplHeap](https://www.php.net/manual/en/class.splheap.php)
  - SplMaxHeap
  - SplMinHeap
- [SplPriorityQueue](https://www.php.net/manual/en/class.splpriorityqueue.php)
- [SplFixedArray](https://www.php.net/manual/en/class.splfixedarray.php)
- [SplObjectStorage](https://www.php.net/manual/en/class.splobjectstorage.php)

```php
$list = new SplDoublyLinkedList();
$list->push('a');
$list->push('b');
$list->push('c');
$list->push('d');

$q = new SplStack();
$q[] = 1;
$q[] = 2;
$q[] = 3;
foreach ($q as $elem)  {
 echo $elem."\n";
}

$queue = new SplQueue();
$queue->enqueue('first');
$queue->enqueue('second');
$queue->enqueue('third');

echo $queue->dequeue(); // Outputs: first
echo $queue->top();     // Outputs: second

$h = new SplMinHeap();
// [parent, child]
$h->insert([0, 1]);
$h->insert([1, 2]);
$h->insert([1, 3]);
$h->insert([1, 4]);

$queue = new SplPriorityQueue();
$queue->insert('a', 3);
$queue->insert('b', 6);
$queue->insert('c', 1);

foreach ($queue as $elem) {
    echo $elem."\n";
}

for ($h->top(); $h->valid(); $h->next()) {
    list($parentId, $myId) = $h->current();
    echo "$myId ($parentId)\n";
}

$array = new SplFixedArray(5);
$array->next();
$array->current();

$s = new SplObjectStorage();
$o1 = new stdClass;
$s->attach($o1);
```

## DS Library

The DS extension is a C based library that provides specialized data structures as an alternative to the PHP array. It is designed to be fast and memory efficient.

### Installation

```bash
pecl install ds
# or 
dnf install php-ds
```
Remember to enable the extension in your `php.ini` file.

### Data Structures

- [Vector](https://www.php.net/manual/en/class.ds-vector.php): Similar to an array, a Vector is a sequence of values in a contiguous buffer that grows automatically. It is more performant in scenarios where you need to frequently append values.
- [Deque](https://www.php.net/manual/en/class.ds-deque.php): A double-ended queue that allows elements to be added or removed from both the front and the back of the sequence. It is optimized for scenarios where you need to manipulate both ends.
- [Map](https://www.php.net/manual/en/class.ds-map.php): An ordered dictionary that maps keys to values. It allows for any type as keys, maintaining order by insertion.
- [Set](https://www.php.net/manual/en/class.ds-set.php): A collection of unique values. This structure is optimized for finding and checking for the existence of values.
- PriorityQueue: Similar to a heap where each value has a priority, and the order of values is determined by their priority.
- [Stack](https://www.php.net/manual/en/class.ds-stack.php): A last in, first out (LIFO) data structure. It is optimized for cases where you only need to add or remove elements from one end.
- [Queue](https://www.php.net/manual/en/class.ds-queue.php): A first in, first out (FIFO) data structure, ideal for scenarios where elements need to be processed in the order they were added.

```php
$vector = new \Ds\Vector();

$vector->push('a');
$vector->push('b', 'c');
$vector[] = 'd';

$map = new \Ds\Map();

$map->put('a', 1);
$map->put('b', 2);
$map['c'] = 3;


```
