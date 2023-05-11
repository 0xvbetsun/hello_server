# 53 Rust Interview Questions + Answers

- [Basic Rust interview questions]()
- [Intermediate Rust interview questions]()
- [Advanced Rust interview questions]()

## Basic Rust interview questions

### 1. What is Rust?

Rust is a general-purpose memory-safe high-performance systems programming language.

It enables developers to write correct and maintainable code. Rust can also compile programs for different architectures and systems, including web browsers.


### 2. Why does Rust have high performance?

Rust has high performance because it compiles directly to native machine code. This enables the program to run at full speed since there isn't an interpreter needed to translate the program to machine instructions.

### 3. Why do Rust programs consume a small amount of memory?

Rust allocates the minimum amount of memory required for an operation and only does so when needed. Once the operation finishes, the memory is then deallocated.

This is in contrast to garbage-collected languages where memory may remain allocated until the garbage collector has an opportunity to deallocate the memory.

### 4. How can you use cargo to build and test Rust code?

To use `cargo` to build Rust code, the `build` command gets used:

```sh
cargo build
```

When using `cargo build`, the `--release` flag will build in release mode.

This turns on optimizations and does not include debug code, which makes the compiled program run at its intended speed.

To use `cargo` to test Rust code, the `test` command gets used:

```sh
cargo test
```
After running `cargo test`, a debug version of the program gets built and then the test suite runs.

The results of the tests get displayed as they run, and are marked with a pass or fail. If the test fails, an error message will indicate the cause of the failure.

### 5. What kinds of programs can you write with Rust?

Rust is a general-purpose programming language that is suitable for writing different kinds of programs across a large domain.

Using Rust, you can create web servers, command line programs, databases, audio plugins, text processors, operating systems, device drivers, and more.

Rust's high performance makes it appealing to use when writing real-time applications such as video and audio decoding.

Rust is also a secure programming language, making it a good choice to write software that demands a high level of availability and security, such as server software or cryptographic algorithm implementations.

### 6. What is the difference between a Rust `enum` and `struct`?

While both `enum` and `struct` provide ways to encapsulate data, they do so in different ways.

A `struct` contains fields and every field in the `struct` is present at all times. This makes `struct` appropriate when you need to group data together and have access to all components of that data.

An enum contains variants in which a single variant gets represented at a time.

This makes enum appropriate when you have more than one data component, but only want a single component at a time.

A parser is an example where using an enum makes sense because a token may be one of a predefined number of items.

[Learn more about Enums in Rust here.](https://academy.zerotomastery.io/courses/1363752/lectures/31612454)

### 7. Provide an example of an `impl` block in Rust

An `impl` block allows implementing functionality on a Rust `enum` or `struct`.

When functionality gets implemented in this way, the functionality becomes bound to the `enum` or `struct`. This helps to encapsulate functionality that is specific to the given `enum` or `struct`.

Here is an example of an `impl` block in Rust implementing functionality to create a new `struct`:

```rust
struct Number(i32);

impl Number { 
    pub fn new(n: i32) -> Self { 
        Self(n) 
    } 
}

let five = Number::new(5);
```

### 8. How do you create an infinite loop in Rust?

Using the Rust keyword `loop` will create an infinite loop:

```rust
loop { 
    // ... 
}
```
Using the `break` keyword will exit the loop.

### 9. How can you mutate variables in Rust?

By default, all data in Rust is **immutable** and cannot get changed without being marked as **mutable**.

Using the `mut` keyword changes this behavior and allows changing (mutating) the data

```rust
let mut a = 0; // mutable 
let b = 0; // immutable
```

### 10. What happens to borrowed data at the end of a Rust function?

When writing a function that **borrows** data, the borrowed data will remain available for use after the function ends. This is because ownership of the data does not transfer when borrowed.

### 11. What happens to owned data at the end of a Rust function?

When writing a function that takes **ownership** of data, the data gets dropped (deleted) at the end of a function.

This is because all owned data gets dropped at the end of a scope, and the end of a function marks the end of a scope.

### 12. What does `#[derive(Debug)]` do in Rust?

Using `#[derive(Debug)]` allows a `struct` or `enum` to get printed with the debug formatting token `{:?}` in the `println!` and `format!` macros.

### 13. What's the difference between `.unwrap()` and .`expect()` in Rust?

Both `.unwrap()` and `.expect()` will trigger a panic if they execute.

`.unwrap()` triggers a thread panic and then displays the line number containing the call to `.unwrap()`.

`.expect()` triggers a thread panic with a customized message, and then displays the line number containing the call to `.expect()`.

### 14. Why is the `return` keyword in Rust optional? Provide examples

The `return` keyword is optional in Rust because Rust is an expression-based language.

Expressions get evaluated and then the result of the evaluation propagates outwards.

This is different when compared to other programming languages that use statements. Statements take some action and then nothing happens at the end of the statement. When using data with statements, extra keywords help to facilitate propagation.

Here is an example of a function that omits the `return` keyword:

```rust
fn one() -> u32 { 1 }
```
Here is an example of a function that uses the `return` keyword:

```rust
fn two() -> u32 { return 2; }
```
The `return` keyword is for returning early from a function. If there isn't a need to return early, then the omitting `return` keyword is appropriate. Leveraging expressions allows the Rust compiler to determine if the branches in the function are all handled properly.

### 15. What is an example of a `match` expression in Rust?

This Rust `match` expression matches an `Option`.

When the `Option` contains `Some`, the data gets printed to the terminal. When the `Option` contains `None`, the message there is no number gets printed to the terminal.

```rust
let foo = Some(1); 

match foo { 
    Some(n) => println!("number is {n}"), 
    None => println!("there is no number"), 
}
```

### 16. Can you assign the result of a Rust `match` expression to a variable binding?

Yes. Since `match` is an expression, assigning the result gets accomplished like this:

```rust
let t = true; 

let one = match t { 
    true => 1, 
    false => 0, 
};
```

### 17. What happens if you add a new variant to a Rust `enum` without changing any other code?

Adding a new variant to an `enum` without changing any other code may trigger compiler errors elsewhere in the program.

When using `match` on an `enum`, all variants must get checked.

Adding a new variant to the `enum`, without updating the `match` blocks which use the `enum`, will trigger compiler errors. This is because the `match` expression no longer handles all possible variants, but this applies solely when the `match` block does not have a **"catch-all"** match arm.

### 18. What Rust keyword will iterate through a collection?

Using the `for` will iterate through a collection:

```rust
let nums = vec![1, 2, 3]; 

for n in nums { 
    println!("{n}") 
}
```

In order for the iteration to occur, the collection must implement the `Iterator` trait

### 19. What Rust code would you write for printing information to the terminal?

Using the `println!` macro will print information to the terminal:

```rust
println!("hello world");
```

The `dbg!` macro is also capable of printing information to the terminal, but should get used solely for debugging purposes:

```rust
let life = 42; 
dbg!(life);
```

### 20. What's a Rust `Vec` and when would you use it?

A `Vec` is a linear collection of elements, with similarities to a dynamic array present in other languages.

`Vec` allows iteration over elements, indexing into the `Vec`, retrieving elements at a given index, and much more.

You would use a `Vec` when you need to store elements in a defined order, or when you plan on iterating over the elements.

## Intermediate Rust interview questions

### 21. Can you create more than one variable using one line of Rust code?

Yes, to create more than one variable in one line of Rust code, a **destructuring** operation needs to occur.

The following code will create variables `a` and `b` by destructuring the tuple `(1, 2)`:

```rust
let (a, b) = (1, 2);
```
It's not possible to declare more than one uninitialized variable in a single line of code.

### 22. What is a Rust trait?

**Traits** in Rust provide a way to declare that some behavior exists.

The implementation of that behavior is specific to the data that implements the trait. It's like creating an interface where the interface dictates what can happen and the implementation dictates how it happens.

### 23. What are generics in Rust?

Rust **generics** provide a way to create `structures`, `enums`, or `functions` that do not know what data they will be working with.

When used with generics, traits act as **generic constraints**, and these constraints declare what kinds of data may get used with the function.

Once the `structure`, `enum`, or `function` uses some data, the compiler will check that the data implements the required traits indicated in the generic constraints.

If the data meets all the requirements, then it gets accepted. If not, a compiler error occurs.

### 24. How can you borrow data in a Rust structure?

Using borrowed data within a Rust structure requires the use of lifetime annotations.

Lifetime annotations tell the compiler that we are borrowing some data from another part of the program:

```rust
#[derive(Debug)]
struct Name<'a> { 
    name: &'a str, 
}

let name = String::from("Bob");
let n = Name { name: &name };
```
In the above example, the `Name` structure borrows a `&str`.

The lifetime of the `&str` is `'a`. Seeing a lifetime in a struct informs developers that some data needs to already exist before creating the structure.

### 25. Is there a way to continue an outer loop from an inner loop in Rust?

Yes, Rust support continuing an outer loop when executing an inner loop through the use of [loop labels](https://doc.rust-lang.org/rust-by-example/flow_control/loop/nested.html):

```rust
let mut b = 0;
'outer: loop {
    'inner: loop {
        if b == 3 {
            continue 'outer;
        }
        b += 1;
    }
}
```
Using loop labels with the `break` keyword instead of `continue` will enable an inner loop to exit both an inner and outer loop.

### 26. What does the Rust question mark operator do?

The question mark operator in Rust offers a convenient way to handle errors or missing data.

When used with `Result`, the question mark operator will either:

- unwrap an `Ok`
- or `return` an `Err`
- 
When it's used with `Option`, it will either:

- unwrap a `Some`
- or `return` a `None`
Because the question mark operator potentially returns values, the function signature must have either `Result` or `Option` set as the return type.

### 27. Write an example of a generic Rust function

This Rust function is generic over all types that implement the `std::fmt::Debug` trait, which allows them to print in a debug context:

```rust
#[derive(Debug)]
struct Sample;
struct Whoops;

debug_print(Sample); 
debug_print("test");
debug_print(Whoops); // compiler error 
```
In the last line of the example the `Whoops` data structure does not implement `Debug`. This line will trigger a compiler error since it does not meet the constraints set by the `debug_print` function.

### 28. Write an example of a generic Rust structure

This generic Rust structure wraps a `Vec` and exposes a single `push` function which allows pushing data to the inner `Vec`.

It has no generic constraints, so it operates on all types

```rust
impl<T> Container<T> { 
    pub fn push(&mut self, item: T) { 
        self.inner.push(item); 
    } 
}

let mut container = Container { inner: vec![] }; 
container.push("sample"); 
```

### 29. Provide a Rust trait example

Here is an example of creating and implementing a trait in Rust:

```rust
struct Dog;

impl Speak for Dog { 
    fn speak() { 
        println!("bark bark!") 
    } 
} 
```
The `speak` function on the `Speak` trait doesn't get defined, making it a required function to implement. The `Dog` structure implements the `Speak` trait by printing **bark bark!** whenever the function gets called.

### 30. What are the different types of Rust closures?

Rust has three different types of closures: `Fn`, `FnOnce`, and `FnMut`.

`Fn` closures can get called any number of times and they operate solely on immutable data.

`FnOnce` closures can get called a single time. This happens if a closure moves data out of its body.

`FnMut` closures can get called any number of times and may mutate captured data.

### 31. What are the differences between a Rust `String` and `&str`?

A Rust `String` is an owned string that is heap-allocated, while a `&str` is a borrowed data type.

Since `String` is an owned data type, the methods implemented on it focus on manipulation of the `String` contents.

`&str` is a borrowed data type, so the implemented functionality focuses on reading and searching the string data.

### 32. Describe the type state pattern in Rust

The [type state pattern](http://cliffle.com/blog/rust-typestate/) utilizes the type system in Rust to define a state machine.

Each state in the state machine gets represented with a Rust `struct`, and transitions get represented using function calls. These function calls return the defined state `structs` and are the sole points where transitions occur.

This prevents outside code from both instantiating an incorrect state machine and performing incorrect state transitions.

### 33. Describe the Rust new type pattern

The [new type pattern](https://doc.rust-lang.org/rust-by-example/generics/new_types.html) in Rust takes an existing type and wraps it in a type created by the developer.

The purpose of using the new type pattern is to implement traits on existing types and to provide interfaces that are relevant to the application.

### 34. What's the difference between `.iter()` and `.into_iter()`?

`.iter()` creates an iterator over a collection.

The items produced by the iterator get borrowed from the original collection, leaving it intact. This is useful when you need to keep a copy of the original data.

`.into_iter()` also creates an iterator over a collection, but instead takes ownership of the collection and moves the items out of the collection.

This is useful when the original data is no longer needed, or if the data needs to be moved to another location (like into a thread).

### 35. How can you convert a Rust `Option` into a `Result`?

The most succinct way to convert an `Option` into a `Result` is to use `.ok_or_else()`:

```rust
let foo: Option<i32> = Some(1); 
let foo: Result<i32, &str> = foo.ok_or_else(|| "no number provided");
```
The `.ok_or_else()` method will convert an `Option` into a `Result`.

When the `Option` is `None`, then the closure provided to `.ok_or_else()` gets run, and the result from running the closure gets wrapped within the `Err` variant of `Result`.

### 36. How can you convert a `Result` into an `Option` in Rust?

Converting a `Result` into an `Option` gets accomplished using the `.ok()` method available on `Result`:

```rust
let foo: Result<i32, ()> = Ok(1); 
let foo: Option<i32> = foo.ok();
```
Since the `None` variant on `Option` doesn't have any data associated with it, converting a `Result` into an `Option` discards all error information (if any) contained within the `Err` variant of the `Result`

### 37. Explain the `.map()` function on Rust's `Iterator` trait

The `.map()` function on `Iterator` performs a transformation on all items within the iterator. The input to `.map()` is the item in the current iteration, and the output from `.map()` is the transformed item.

Here is an example that iterates over some numbers and uses `.map()` to double the value of each number:

```rust
let nums = vec![1, 2, 3]; 
let doubled = nums.iter().map(|n| n * 2);
```

### 38. What function converts a Rust iterator into a `Vec`?

Converting a Rust iterator into a `Vec` makes use of the `.collect()` function:

```rust
let nums = vec![1, 2, 3]; 
let doubled = nums.iter()
                  .map(|n| n * 2)
                  .collect::<Vec<_>>();
```
The `.collect()` function "collects" all the items in the iterator and creates a new data structure containing the items. This works solely on data structures that implement the `Iterator` trait.

### 39. What's a `HashMap` in Rust and when would you use it?

A `HashMap` is a collection consisting of key/value pairs.

The keys get used to locate elements within the `HashMap`, and the values are the data associated with each key.

Since `HashMap` uses key accesses, it's a great data structure to use when you want to randomly access data and you have the key available.

### 40. How can you create nested functions in Rust?

Creating a nested function in Rust is the same as creating a non-nested function. Use the `fn` keyword within an existing function to create a nested one:

```rust
fn outer() -> bool { 
    fn inner() -> bool { 
        true 
    } 
    inner() 
}
```

## Advanced Rust interview questions

### 41. How does the Rust question mark operator convert errors to the correct type?

During code compilation, the question mark operator gets converted into a `match` expression. In the `Err` arm, the `Into` trait gets used to convert the error into the appropriate type.

Here is an example of what code the question mark operator generates:

```rust
let foo = match bar() { 
    Ok(f) = f, 
    Err(e) => return Err(e.into()) 
};
```

### 42. Write a Rust function signature that can accept `String`, `&str`, `Path`, and `PathBuf` using a single parameter

A Rust function that accepts different types using a single function parameter requires the use of generics. Here is an example:

```rust
fn sample<P: AsRef<Path>>(p: P) { 
    // ...
}
```
The `AsRef` trait can convert `String`, `&str`, and `PathBuf` to a `Path` because there are implementations of `AsRef` on these types to perform the conversion.

### 43. How would you create a Rust iterator from a data structure you made?

There are two ways to create an iterator when working with your own Rust data structures.

If the data structure contains another data structure that implements `Iterator`, then using the other data structure's `.iter()` method is a quick way to enable iteration.

```rust
impl Foo { 
    pub fn iter(&self) -> impl Iterator<Item = &usize> { 
        self.inner.iter() 
    } 
}
```
If there is no inner data structure that implements `Iterator`, then `Iterator` needs to get implemented.

Here is an example of an iterator which that computes fibonacci numbers:

```rust 
impl Fibonacci { 
    pub fn new(n: u64) -> Self { 
        Self { n } 
    } 
}
impl Fibonacci { 
    fn fibonacci(n: u64) -> u64 { 
        match n { 
            0 => 1, 
            1 => 1, 
            _ => Self::fibonacci(n - 1) + Self::fibonacci(n - 2), 
        } 
    } 
}
impl Iterator for Fibonacci { 
    type Item = u64;

    fn next(&mut self) -> Option<Self::Item> {
        let next = Some(Self::fibonacci(self.n));
        self.n += 1;
        next
    }
}
let fib = Fibonacci::new(0); 
for f in fib { 
    // ... 
} 
```

### 44. Give an example of when would you use `Arc` in Rust

`Arc` in Rust gets used when multiple threads need access to some data.
**For example**
There can be some global configuration data that needs sharing across multiple threads. Using an `Arc` allows all threads to access this data:

```rust
#[derive(Clone)]
struct Config { 
    path: Arc<PathBuf>, 
}
```
Now that the `path` is protected by an `Arc`, sharing the data is safe to do between different threads.

### 45. Is it possible to create a Rust `Vec` that contains different data types? Provide examples

Yes, different data types can exist within a single `Vec` in Rust.

The data must get converted into **trait objects** and then accessed using **dynamic dispatch**:

```rust
#[derive(Debug)]
struct Foo;

#[derive(Debug)]
struct Bar;

fn print(d: &dyn fmt::Debug) { 
    println!("{d:?}"); 
}

let items: Vec<Box<dyn fmt::Debug>> = vec![Box::new(Foo), Box::new(Bar)]; 
for i in items { 
    print(&i); 
}
```

### 46. What are the performance implications of using trait objects and dynamic dispatch in Rust?

Using trait objects and dynamic dispatch incurs some overhead.

Trait objects get stored on the heap, and accessing them requires a pointer indirection. When running functions implemented on trait objects using dynamic dispatch, another pointer indirection occurs.

Compared to stack-allocated non-dynamic data, trait objects will be slower because of multiple pointer indirections and heap-only memory accesses.

### 47. What is a Rust supertrait?

A [supertrait](https://doc.rust-lang.org/rust-by-example/trait/supertraits.html) in Rust is a combination of two or more traits.

When a supertrait gets set as a trait bound, all traits that compose the supertrait require implementations on the type.

```rust
// supertrait 
trait FooBar: Foo + Bar{}

impl Foo for A { 
    fn foo(&self) { 
        println!("A foo") 
    } 
}
impl Bar for A { 
    fn bar(&self) { 
        println!("A bar") 
    } 
}
impl FooBar for A {}

fn foobar(f: impl FooBar) { 
    f.foo(); 
    f.bar(); 
}

fn main() { 
    let a = A; 
    foobar(a); 
} 
```

### 48. When would you use a Rust declarative macro?

[Declarative macros](https://doc.rust-lang.org/book/ch19-06-macros.html) are useful in Rust when you need to write multiple blocks of code where each block contains similar code.

Examples of when to use declarative macros include writing `impl` blocks, or encapsulating control flow.

It's also possible to use declarative macros to create domain-specific languages (DSL).

DSLs are useful because the syntax of the DSL is customizable when creating the macro. This can help make otherwise complicated code easier to work with.

### 49. Write a Rust macro to implement a trait for a list of different types

This Rust declarative macro repeats an `impl` block for each type provided:

```rust
macrorules! implspeak { 
    ( $( $type:ty => $msg:literal )+ ) => { 
        $( impl Speak for $type { 
            fn speak(&self) { 
                println!($msg); 
            } 
        } )+ 
    } 
}
struct Dog; 
struct Cat; 
struct Bird;

impl_speak! { 
    Dog => "bark bark" 
    Cat => "meow" 
    Bird => "tweet tweet" 
} 
```

### 50. Write an example of the type state pattern in Rust using generics

The Rust generic type state pattern is useful when you want to preserve data across multiple states.

In this example, a cruise control system for a car can transition between `On`, `Off`, and `Suspended`.

The cruise control speed remains available across different states during transitions:

```rust
// Allow adding Speed 
impl std::ops::AddAssign for Speed { 
    fn addassign(&mut self, rhs: Self) { 
        self.0.saturatingadd(rhs.0); 
    } 
}
// Allow subtracting Speed 
impl std::ops::SubAssign for Speed { 
    fn subassign(&mut self, rhs: Self) { 
        self.0.saturatingsub(rhs.0); 
    } 
}

// trait that all states must implement 
trait Cruising {}

// states 
struct Off; 
struct On; 
struct Suspended;

// enable usage in the state container 
impl Cruising for Off {} 
impl Cruising for On {} 
impl Cruising for Suspended {}

// state container 
struct CruiseControl<T: Cruising> { 
    // current state 
    state: T, 
    // target cruising speed 
    target: Speed, 
}

// transition function usable by all states 
impl<T: Cruising> CruiseControl<T> { 
    fn transition<N: Cruising>(self, next: N) -> CruiseControl<N> { 
        CruiseControl { target: self.target, state: next, } 
    } 
}

impl CruiseControl<Off> { 
    fn engage(target: Speed) -> CruiseControl<On> { 
        CruiseControl { state: On, target } 
    } 
}
impl CruiseControl<On> { 
    pub fn speedincrease(&mut self, amount: Speed) { 
        self.target += amount; 
    } 
    pub fn speeddecrease(&mut self, amount: Speed) { 
        self.target -= amount; 
    } 
    pub fn suspend(self) -> CruiseControl<Suspended> { 
        self.transition(Suspended) 
    } 
    pub fn disengage(self) -> CruiseControl<Off> { 
        self.transition(Off) 
    } 
}
impl CruiseControl<Suspended> { 
    pub fn resume(self) -> CruiseControl<On> { 
        self.transition(On) 
    } 
    pub fn resumeattarget(self, target: Speed) -> CruiseControl<On> { 
        // update to new target 
        let mut control = self; 
        control.target = target; 
        control.transition(On) 
    } 
    pub fn disengage(self) -> CruiseControl<Off> { 
        self.transition(Off) 
    } 
}
```

### 51. Why does this Rust code fail to compile when using threads?

```rust
fn sample() { 
    let mut i = 0; 
    std::thread::spawn(|| { i += 1; }); 
}
```

This Rust code fails to compile because the `sample` function has ownership of the `i` variable.

When the `sample` function ends, the `i` variable will get destroyed. The thread spawned may continue to live even though the sample function is complete and destroyed `i`.

For this reason, it would be unsafe to mutate `i` since it may no longer exist by the time the thread gets the opportunity to make any updates to the variable.

To fix this error, `i` has to move into the thread

```rust
fn sample() { 
    let mut i = 0; 
    std::thread::spawn(move || { i += 1; }); 
}
```
Once `i` gets moved into the thread, the `sample` function no longer has ownership of `i` and cannot delete it. This enables the thread to mutate `i`.

### 52. How can you add a dependency from a `git` repository instead of a crate registry?

In the `Cargo.toml` file, a dependency can be set to use a git repository by using the `git` key:

```toml
[dependencies] 
serde = { git = "https://github.com/serde-rs/serde", features = ["derive"] }
```

### 53. What are cargo workspaces?

[Cargo workspaces](https://doc.rust-lang.org/book/ch14-03-cargo-workspaces.html) provide a way to group crates under a single directory and have them get managed by cargo.

This allows using a single cargo command to build and test the crates in the workspace without the need to jump between different projects. The crates all use a single `target` directory, sharing artifacts across projects.

To make a workspace, create a `Cargo.toml` in an empty directory with the following content:

```toml
members = [ "crateone", "anothercrate", "three" ]
```

Each item in the `members` array should be a folder containing a Rust crate with its own `Cargo.toml` file.

After creating this file, `cargo` commands will automatically operate on the entire workspace.