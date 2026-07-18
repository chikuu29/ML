# Python Interview Questions & Answers

---

# 1. Explain Python Memory Management

## Answer

Python automatically manages memory using **reference counting** and a **garbage collector (GC)**.

### How it works

### 1. Memory Allocation

When an object is created,

```python
a = [1, 2, 3]
```

Python allocates memory from its private heap.

Only the Python memory manager can access this heap.

---

### 2. Reference Counting

Every object keeps track of how many variables reference it.

Example

```python
a = [1,2,3]
b = a
```

Reference Count = 2

```
a ─────► [1,2,3] ◄───── b
```

If

```python
del a
```

Reference Count = 1

When Reference Count becomes 0,

Python immediately frees the memory.

---

### 3. Garbage Collection

Reference counting cannot clean **circular references**.

Example

```python
class A:
    pass

x = A()
y = A()

x.ref = y
y.ref = x
```

Even after

```python
del x
del y
```

Objects still reference each other.

Python's **Garbage Collector (GC)** detects and removes these cyclic objects.

Import module

```python
import gc
gc.collect()
```

---

### Memory Areas

```
Stack Memory
--------------
Function Calls
Local Variables

Heap Memory
--------------
Objects
Lists
Dictionary
Class Objects
```

---

### Interview One-Liner

> Python manages memory automatically using reference counting and a cyclic garbage collector that cleans objects involved in circular references.

---

# 2. What is GIL?

## Answer

GIL = **Global Interpreter Lock**

It is a mutex that allows **only one thread to execute Python bytecode at a time** in the CPython interpreter.

Even on a multi-core CPU, only one Python thread executes Python code simultaneously.

---

### Why GIL exists?

To make memory management thread-safe.

Without GIL,

multiple threads could modify the same Python object simultaneously.

---

### CPU-bound Example

```python
while True:
    x = x + 1
```

Using 10 threads

↓

Still only one thread executes Python bytecode at a time.

---

### I/O-bound Example

```
Downloading Files

Thread 1 → waiting

Thread 2 → executes

Thread 3 → waiting
```

During I/O waits, the GIL is released, allowing other threads to run.

---

### When to use

Multithreading

✔ Network Calls

✔ API Calls

✔ File Reading

✔ Database Queries

Multiprocessing

✔ Machine Learning

✔ Image Processing

✔ Data Science

✔ Heavy Computation

---

### Interview One-Liner

> The GIL is a lock in CPython that allows only one thread to execute Python bytecode at a time, simplifying memory management but limiting true parallel execution of CPU-bound threads.

---

# 3. Generator vs Iterator

## Iterator

An iterator is an object that implements

```
__iter__()

__next__()
```

Example

```python
nums = iter([1,2,3])

print(next(nums))
print(next(nums))
```

Output

```
1
2
```

---

## Generator

A generator is a simpler way to create an iterator using the **yield** keyword.

Example

```python
def numbers():
    yield 1
    yield 2
    yield 3

g = numbers()

print(next(g))
print(next(g))
```

Output

```
1
2
```

---

### Advantages of Generator

Instead of storing

```
1 million numbers
```

Generator produces

```
one number at a time
```

Memory Efficient

---

### Comparison

| Iterator | Generator |
|-----------|-----------|
| Uses `__iter__()` and `__next__()` | Uses `yield` |
| More code | Less code |
| Manual implementation | Automatic |
| Memory Efficient | More memory efficient due to lazy evaluation |

---

### Interview One-Liner

> Every generator is an iterator, but not every iterator is a generator.

---

# 4. What is a Decorator?

## Answer

A decorator is a function that modifies or extends the behavior of another function without changing its source code.

Syntax

```python
@decorator
def hello():
    pass
```

Equivalent to

```python
hello = decorator(hello)
```

---

### Example

```python
def logger(func):

    def wrapper():
        print("Before")

        func()

        print("After")

    return wrapper


@logger
def greet():
    print("Hello")


greet()
```

Output

```
Before

Hello

After
```

---

### Uses

- Logging
- Authentication
- Authorization
- Timing functions
- Caching (`functools.lru_cache`)
- Input validation

---

### Interview One-Liner

> A decorator wraps another function to add extra functionality without modifying the original function.

---

# 5. What is Lambda?

## Answer

A lambda is a small anonymous function.

Syntax

```python
lambda arguments: expression
```

---

Example

```python
square = lambda x: x*x

print(square(5))
```

Output

```
25
```

---

Used with

```python
map()

filter()

sorted()

reduce()
```

Example

```python
nums = [1,2,3]

result = list(map(lambda x: x*x, nums))

print(result)
```

Output

```
[1,4,9]
```

---

### Interview One-Liner

> A lambda is an anonymous, single-expression function commonly used for short operations and as callbacks.

---

# 6. Deep Copy vs Shallow Copy

### Shallow Copy

Copies only the outer object.

Nested objects are shared.

Example

```python
import copy

a = [[1,2], [3,4]]

b = copy.copy(a)

b[0][0] = 100

print(a)
```

Output

```
[[100,2],[3,4]]
```

Original changed.

---

### Deep Copy

Copies everything recursively.

```python
import copy

a = [[1,2], [3,4]]

b = copy.deepcopy(a)

b[0][0] = 100

print(a)
```

Output

```
[[1,2],[3,4]]
```

Original remains unchanged.

---

### Comparison

| Shallow Copy | Deep Copy |
|---------------|-----------|
| Copies outer object only | Copies nested objects too |
| Shares child objects | Independent child objects |
| Faster | Slower |
| Less memory | More memory |

---

### Interview One-Liner

> A shallow copy duplicates only the outer container, while a deep copy recursively copies all nested objects.

---

# 7. Thread vs Process

| Thread | Process |
|---------|----------|
| Lightweight | Heavyweight |
| Shared memory | Separate memory |
| Faster creation | Slower creation |
| Communication is easy | Requires IPC (Inter-Process Communication) |
| Affected by the GIL in CPython | Not affected by the GIL |

---

### Thread Example

```
Program

├── Thread 1

├── Thread 2

└── Thread 3
```

Shared memory

---

### Process Example

```
Program

├── Process 1

├── Process 2

└── Process 3
```

Each has its own memory space.

---

### Use Cases

Threads

- API Calls
- File Downloads
- Database Calls

Processes

- Machine Learning
- Data Science
- Video Processing
- Image Processing

---

### Interview One-Liner

> Threads share the same memory space and are lightweight, while processes have separate memory spaces and are better for CPU-intensive parallel execution.

---

# 8. Async vs Multithreading

## Async

Uses a single thread with an event loop.

Works through

```
async

await
```

Example

```python
import asyncio

async def hello():
    await asyncio.sleep(2)
    print("Done")

asyncio.run(hello())
```

Best for

- HTTP Requests
- FastAPI
- Chat Applications
- High-concurrency I/O

---

## Multithreading

Uses multiple threads managed by the operating system.

Example

```python
from threading import Thread

def task():
    print("Running")

Thread(target=task).start()
```

Best for

- File I/O
- Database Queries
- Background tasks
- Network operations

---

## Comparison

| Async | Multithreading |
|--------|----------------|
| Single thread | Multiple threads |
| Event loop | OS scheduler |
| Cooperative concurrency (`await`) | Preemptive scheduling |
| Low memory usage | Higher memory usage |
| Excellent for many I/O-bound tasks | Good for I/O-bound tasks, but limited by the GIL for CPU-bound Python code |

---

## When to Use

### Use Async

✔ FastAPI

✔ HTTP APIs

✔ WebSockets

✔ Thousands of concurrent requests

### Use Threads

✔ Background jobs

✔ File reading

✔ Database queries

✔ Blocking libraries that don't support async

### Use Processes

✔ AI/ML

✔ Video Encoding

✔ NumPy-heavy computation

✔ CPU-intensive workloads

---

# Interview Summary

| Topic | One-Liner |
|--------|-----------|
| Memory Management | Python uses reference counting and a garbage collector to manage memory automatically. |
| GIL | Allows only one thread to execute Python bytecode at a time in CPython. |
| Generator | Uses `yield` to lazily produce values one at a time. |
| Iterator | Object implementing `__iter__()` and `__next__()`. |
| Decorator | Wraps a function to add behavior without changing its code. |
| Lambda | Anonymous single-expression function. |
| Deep Copy | Recursively copies nested objects. |
| Shallow Copy | Copies only the outer object; nested objects are shared. |
| Thread | Lightweight unit sharing memory with other threads. |
| Process | Independent execution unit with separate memory. |
| Async | Single-threaded, event-loop-based concurrency for I/O-bound tasks. |
| Multithreading | Multiple OS threads for concurrent execution, mainly useful for I/O-bound work in CPython. |