# ☕ Java Core — Complete Learning Roadmap

> A structured guide to mastering Java Core from scratch to interview-ready.
> Each topic links to a dedicated notes file. Check off topics as you complete them.

---

## 📑 Table of Contents

1. [How to Use This Roadmap](#how-to-use-this-roadmap)
2. [Phase 1 — Java Basics](#phase-1--java-basics)
3. [Phase 2 — Object Oriented Programming](#phase-2--object-oriented-programming-oop)
4. [Phase 3 — Core Java Deep Dive](#phase-3--core-java-deep-dive)
5. [Phase 4 — Collections Framework](#phase-4--collections-framework)
6. [Phase 5 — Exception Handling](#phase-5--exception-handling)
7. [Phase 6 — Multithreading & Concurrency](#phase-6--multithreading--concurrency)
8. [Phase 7 — Java 8+ Modern Features](#phase-7--java-8-modern-features)
9. [Phase 8 — File I/O & Serialization](#phase-8--file-io--serialization)
10. [Phase 9 — Interview Must-Knows](#phase-9--interview-must-knows)
11. [Progress Tracker](#progress-tracker)

---

## How to Use This Roadmap

```
① Follow the phases in order — each builds on the previous
② For each topic, write your own notes file (linked below)
③ Practice at least 2-3 problems per topic on LeetCode / GFG
④ Revisit the ⭐ marked topics before every interview
⑤ Don't skip Phase 4 (Collections) — it's asked in 90% of interviews
```

---

## Phase 1 — Java Basics

> **Goal:** Understand the language syntax and how Java works under the hood.

### 1.1 Java Fundamentals
- [ ] What is Java? JDK vs JRE vs JVM
- [ ] How Java code runs — Compile → Bytecode → JVM
- [ ] Writing your first program — `public static void main`
- [ ] `System.out.println` vs `print` vs `printf`
- [ ] Comments — single line, multi-line, Javadoc

### 1.2 Data Types & Variables
- [ ] Primitive types — `int`, `long`, `float`, `double`, `char`, `boolean`, `byte`, `short`
- [ ] Wrapper classes — `Integer`, `Long`, `Double`, `Character`, `Boolean`
- [ ] Auto-boxing and Unboxing
- [ ] `var` keyword (Java 10+)
- [ ] Type casting — implicit vs explicit
- [ ] Overflow and underflow

### 1.3 Operators
- [ ] Arithmetic — `+ - * / %`
- [ ] Relational — `== != > < >= <=`
- [ ] Logical — `&& || !`
- [ ] Bitwise — `& | ^ ~ << >> >>>`
- [ ] Ternary — `condition ? a : b`
- [ ] `instanceof` operator

### 1.4 Control Flow
- [ ] `if`, `else if`, `else`
- [ ] `switch` statement (classic)
- [ ] `switch` expression (Java 14+)
- [ ] `for` loop
- [ ] `while` loop
- [ ] `do-while` loop
- [ ] Enhanced for-each loop
- [ ] `break`, `continue`, `return`
- [ ] Labeled loops

### 1.5 Arrays
- [ ] 1D array — declaration, initialization, access
- [ ] 2D array (matrix) — row × col
- [ ] Jagged arrays
- [ ] `Arrays` utility class — `sort`, `fill`, `copyOf`, `binarySearch`
- [ ] Array vs ArrayList

---

## Phase 2 — Object Oriented Programming (OOP)

> **Goal:** Master the four pillars of OOP and how Java implements them. ⭐ _Heavy interview territory._

### 2.1 Classes & Objects
- [ ] Class definition — fields, methods, constructors
- [ ] Creating objects — `new` keyword
- [ ] `this` keyword
- [ ] `static` keyword — static fields, static methods, static blocks
- [ ] `final` keyword — final variables, final methods, final classes

### 2.2 Constructors
- [ ] Default constructor
- [ ] Parameterized constructor
- [ ] Constructor overloading
- [ ] Constructor chaining — `this()` and `super()`
- [ ] Copy constructor

### 2.3 Encapsulation ⭐
- [ ] Access modifiers — `public`, `private`, `protected`, default
- [ ] Getters and Setters
- [ ] Why encapsulation matters

### 2.4 Inheritance ⭐
- [ ] `extends` keyword
- [ ] Single inheritance
- [ ] Multilevel inheritance
- [ ] `super` keyword — accessing parent fields and methods
- [ ] Method overriding — `@Override`
- [ ] Why Java doesn't support multiple inheritance
- [ ] `Object` class — the root of all classes

### 2.5 Polymorphism ⭐
- [ ] Compile-time (static) — method overloading
- [ ] Runtime (dynamic) — method overriding
- [ ] Upcasting and Downcasting
- [ ] Dynamic Method Dispatch

### 2.6 Abstraction ⭐
- [ ] Abstract classes — `abstract` keyword
- [ ] Abstract methods
- [ ] Interfaces — `interface` keyword
- [ ] `default` and `static` methods in interfaces (Java 8+)
- [ ] Abstract class vs Interface — when to use which

### 2.7 Important OOP Concepts
- [ ] `instanceof` for type checking
- [ ] Object class methods — `equals()`, `hashCode()`, `toString()`, `clone()`
- [ ] Overriding `equals()` and `hashCode()` — the contract ⭐
- [ ] Shallow copy vs Deep copy
- [ ] Immutable classes — how to create one ⭐

---

## Phase 3 — Core Java Deep Dive

> **Goal:** Understand how Java manages memory, strings, and type system.

### 3.1 String ⭐
- [ ] String creation — literal vs `new String()`
- [ ] String pool (intern pool) — how it works
- [ ] String immutability — why strings are immutable
- [ ] String methods — all operations (see your String notes)
- [ ] `String` vs `StringBuilder` vs `StringBuffer`
- [ ] `StringBuilder` — when and why to use
- [ ] `String.format()` and formatted output
- [ ] `toCharArray()` and character iteration
- [ ] String comparison — `equals()` vs `==`

### 3.2 Memory Management
- [ ] Stack vs Heap memory
- [ ] How objects are stored
- [ ] Garbage Collection — what it is, how it works
- [ ] `System.gc()` — hint to GC
- [ ] Memory leaks in Java

### 3.3 Packages & Imports
- [ ] What is a package
- [ ] `import` statement
- [ ] `java.lang` — auto-imported package
- [ ] Wildcard import `import java.util.*`
- [ ] Creating your own packages

### 3.4 Enums
- [ ] Basic enum definition
- [ ] Enum with fields and methods
- [ ] `values()`, `ordinal()`, `name()`
- [ ] Enum in switch statement
- [ ] EnumSet and EnumMap

### 3.5 Generics ⭐
- [ ] What are generics and why
- [ ] Generic classes — `class Box<T>`
- [ ] Generic methods
- [ ] Bounded type parameters — `<T extends Number>`
- [ ] Wildcards — `<?>`, `<? extends T>`, `<? super T>`
- [ ] Type erasure — what happens at runtime

### 3.6 Nested Classes
- [ ] Static nested class
- [ ] Inner class (non-static)
- [ ] Local class (inside a method)
- [ ] Anonymous class

---

## Phase 4 — Collections Framework

> **Goal:** Master every data structure Java provides. ⭐ _Most asked in interviews._

```
java.util.Collection hierarchy:

     Collection
    /     |     \
  List   Set    Queue
   |    / | \     \
  ...  /  |  \   Deque
```

### 4.1 List Interface
- [ ] `ArrayList` — dynamic array, random access, O(1) get
- [ ] `LinkedList` — doubly linked list, O(1) add/remove at ends
- [ ] `Vector` — legacy, synchronized ArrayList
- [ ] `Stack` — legacy, use `Deque` instead
- [ ] List methods — `add`, `remove`, `get`, `set`, `subList`, `sort`
- [ ] `Collections` utility class — `sort`, `reverse`, `shuffle`, `min`, `max`

### 4.2 Set Interface ⭐
- [ ] `HashSet` — hash table, no order, O(1)
- [ ] `LinkedHashSet` — insertion order, O(1)
- [ ] `TreeSet` — sorted, Red-Black tree, O(log n)
- [ ] Set operations — union, intersection, difference
- [ ] Internal working of all three

> 📄 See: `Java_Sets_Maps_Complete_Guide.md`

### 4.3 Map Interface ⭐
- [ ] `HashMap` — hash table, no order, O(1)
- [ ] `LinkedHashMap` — insertion order, LRU Cache
- [ ] `TreeMap` — sorted keys, Red-Black tree, O(log n)
- [ ] `Hashtable` — legacy, synchronized
- [ ] `ConcurrentHashMap` — thread-safe modern alternative
- [ ] Map methods — `put`, `get`, `remove`, `containsKey`, `entrySet`, `getOrDefault`, `merge`
- [ ] Internal working of all three

> 📄 See: `Java_Sets_Maps_Complete_Guide.md`

### 4.4 Queue & Deque
- [ ] `Queue` interface — FIFO
- [ ] `PriorityQueue` — heap-based, min-heap by default
- [ ] `PriorityQueue` with custom comparator — max-heap
- [ ] `Deque` interface — double-ended queue
- [ ] `ArrayDeque` — use instead of Stack and Queue
- [ ] `LinkedList` as Queue and Deque

### 4.5 Collections Utility Class
- [ ] `Collections.sort()`
- [ ] `Collections.binarySearch()`
- [ ] `Collections.reverse()`
- [ ] `Collections.unmodifiableList()` / `unmodifiableMap()`
- [ ] `Collections.synchronizedList()`
- [ ] `Collections.frequency()`
- [ ] `Collections.disjoint()`

### 4.6 Iterator & Iterable
- [ ] `Iterator` — `hasNext()`, `next()`, `remove()`
- [ ] `ListIterator` — bidirectional
- [ ] `Iterable` interface — implementing custom iterables
- [ ] `ConcurrentModificationException` — what causes it

---

## Phase 5 — Exception Handling

> **Goal:** Write robust programs that handle errors gracefully.

### 5.1 Exception Basics
- [ ] What is an exception vs error
- [ ] Exception hierarchy — `Throwable → Exception → RuntimeException`
- [ ] Checked vs Unchecked exceptions ⭐
- [ ] `Error` vs `Exception`

### 5.2 Handling Exceptions
- [ ] `try`, `catch`, `finally` blocks
- [ ] Multiple catch blocks
- [ ] Multi-catch — `catch (IOException | SQLException e)`
- [ ] `finally` — always runs (even with return)
- [ ] `try-with-resources` — auto-closing (Java 7+) ⭐

### 5.3 Throwing Exceptions
- [ ] `throw` — throw an exception manually
- [ ] `throws` — declare checked exceptions
- [ ] Creating custom exceptions

### 5.4 Common Exceptions to Know
- [ ] `NullPointerException`
- [ ] `ArrayIndexOutOfBoundsException`
- [ ] `ClassCastException`
- [ ] `NumberFormatException`
- [ ] `StackOverflowError`
- [ ] `OutOfMemoryError`
- [ ] `IllegalArgumentException`
- [ ] `ConcurrentModificationException`

---

## Phase 6 — Multithreading & Concurrency

> **Goal:** Understand how Java handles parallel execution. ⭐ _Asked in senior roles._

### 6.1 Thread Basics
- [ ] What is a thread vs process
- [ ] Creating threads — `extends Thread` vs `implements Runnable`
- [ ] `Thread` lifecycle — New → Runnable → Running → Blocked → Dead
- [ ] `start()` vs `run()`
- [ ] `sleep()`, `join()`, `yield()`
- [ ] Thread priority

### 6.2 Synchronization ⭐
- [ ] Race condition — what and why
- [ ] `synchronized` keyword — method and block level
- [ ] Intrinsic locks (monitors)
- [ ] `volatile` keyword
- [ ] Deadlock — what it is and how to avoid it
- [ ] `wait()`, `notify()`, `notifyAll()`

### 6.3 Executor Framework (Java 5+) ⭐
- [ ] `ExecutorService` — thread pool management
- [ ] `Executors.newFixedThreadPool()`
- [ ] `Executors.newCachedThreadPool()`
- [ ] `Callable` vs `Runnable`
- [ ] `Future` — get async results
- [ ] `submit()` vs `execute()`
- [ ] Shutting down an executor

### 6.4 Concurrent Collections
- [ ] `ConcurrentHashMap`
- [ ] `CopyOnWriteArrayList`
- [ ] `BlockingQueue` — `ArrayBlockingQueue`, `LinkedBlockingQueue`
- [ ] `AtomicInteger`, `AtomicLong`, `AtomicReference`

---

## Phase 7 — Java 8+ Modern Features

> **Goal:** Write modern, clean Java using functional programming. ⭐ _Must-know for any Java role._

### 7.1 Lambda Expressions ⭐
- [ ] What is a lambda
- [ ] Syntax — `(params) -> expression`
- [ ] Replacing anonymous classes with lambdas
- [ ] Effectively final variables in lambdas

### 7.2 Functional Interfaces ⭐
- [ ] `@FunctionalInterface`
- [ ] `Function<T, R>` — takes T, returns R
- [ ] `Predicate<T>` — takes T, returns boolean
- [ ] `Consumer<T>` — takes T, returns nothing
- [ ] `Supplier<T>` — takes nothing, returns T
- [ ] `BiFunction`, `BiPredicate`, `BiConsumer`
- [ ] Method references — `Class::method`

### 7.3 Stream API ⭐
- [ ] What is a Stream — not a data structure!
- [ ] Creating streams — `stream()`, `of()`, `generate()`, `iterate()`
- [ ] Intermediate operations — `filter`, `map`, `flatMap`, `distinct`, `sorted`, `limit`, `skip`
- [ ] Terminal operations — `forEach`, `collect`, `count`, `reduce`, `findFirst`, `anyMatch`
- [ ] `Collectors` — `toList`, `toSet`, `groupingBy`, `joining`, `counting`
- [ ] Parallel streams
- [ ] Primitive streams — `IntStream`, `LongStream`, `DoubleStream`

### 7.4 Optional ⭐
- [ ] What is `Optional` and why
- [ ] `Optional.of()`, `Optional.ofNullable()`, `Optional.empty()`
- [ ] `isPresent()`, `ifPresent()`, `get()`
- [ ] `orElse()`, `orElseGet()`, `orElseThrow()`
- [ ] Chaining with `map()` and `filter()`

### 7.5 Other Java 8+ Features
- [ ] Default methods in interfaces
- [ ] Static methods in interfaces
- [ ] `Map.forEach()`, `Map.computeIfAbsent()`, `Map.merge()`
- [ ] `Comparator` chaining — `thenComparing()`
- [ ] Date and Time API — `LocalDate`, `LocalTime`, `LocalDateTime` (Java 8)
- [ ] Text Blocks (Java 15)
- [ ] Records (Java 16) ⭐
- [ ] Sealed classes (Java 17)
- [ ] Pattern matching for `instanceof` (Java 16)

---

## Phase 8 — File I/O & Serialization

> **Goal:** Read and write files and understand object persistence.

### 8.1 File I/O
- [ ] `File` class — create, delete, check existence
- [ ] `FileReader` / `FileWriter` — character streams
- [ ] `BufferedReader` / `BufferedWriter` — efficient reading
- [ ] `FileInputStream` / `FileOutputStream` — byte streams
- [ ] Reading line by line — `BufferedReader.readLine()`
- [ ] `Files` utility class (Java NIO) — `readAllLines`, `write`, `copy`
- [ ] `Path` and `Paths` (NIO)

### 8.2 Serialization
- [ ] What is serialization
- [ ] `Serializable` interface
- [ ] `ObjectOutputStream` / `ObjectInputStream`
- [ ] `transient` keyword — skip fields during serialization
- [ ] `serialVersionUID` — why it matters
- [ ] Deserialization risks

---

## Phase 9 — Interview Must-Knows

> **Goal:** Nail the topics that come up in 80% of Java interviews.

### 9.1 JVM Internals ⭐
- [ ] JVM Architecture — ClassLoader, Method Area, Heap, Stack, PC Register
- [ ] Class loading — Bootstrap, Extension, Application classloader
- [ ] Just-In-Time (JIT) compilation
- [ ] Garbage collection algorithms — Serial, Parallel, G1, ZGC
- [ ] `finalize()` method (deprecated but still asked)

### 9.2 Design Patterns ⭐
- [ ] Singleton pattern (thread-safe)
- [ ] Factory pattern
- [ ] Builder pattern
- [ ] Observer pattern
- [ ] Strategy pattern

### 9.3 SOLID Principles ⭐
- [ ] S — Single Responsibility
- [ ] O — Open/Closed
- [ ] L — Liskov Substitution
- [ ] I — Interface Segregation
- [ ] D — Dependency Inversion

### 9.4 Key Interview Topics Recap
- [ ] `==` vs `equals()` vs `hashCode()`
- [ ] String pool and `intern()`
- [ ] `final` vs `finally` vs `finalize()`
- [ ] `abstract class` vs `interface`
- [ ] Checked vs unchecked exceptions
- [ ] `ArrayList` vs `LinkedList` — when to use which
- [ ] `HashMap` internal working — full explanation
- [ ] How `ConcurrentHashMap` achieves thread safety
- [ ] What is immutability — how to create an immutable class
- [ ] What is a memory leak in Java — how to detect

---

## Progress Tracker

```
Phase 1 — Java Basics              [ ] Not Started  [ ] In Progress  [ ] Done
Phase 2 — OOP                      [ ] Not Started  [ ] In Progress  [ ] Done
Phase 3 — Core Java Deep Dive      [ ] Not Started  [ ] In Progress  [ ] Done
Phase 4 — Collections Framework    [ ] Not Started  [ ] In Progress  [ ] Done
Phase 5 — Exception Handling       [ ] Not Started  [ ] In Progress  [ ] Done
Phase 6 — Multithreading           [ ] Not Started  [ ] In Progress  [ ] Done
Phase 7 — Java 8+ Features         [ ] Not Started  [ ] In Progress  [ ] Done
Phase 8 — File I/O                 [ ] Not Started  [ ] In Progress  [ ] Done
Phase 9 — Interview Must-Knows     [ ] Not Started  [ ] In Progress  [ ] Done
```

---

## 📁 Notes File Index

| File | Topics Covered |
|---|---|
| `Java_Core_README.md` | This file — full roadmap |
| `Java_Sets_Maps_Complete_Guide.md` | HashSet, LinkedHashSet, TreeSet, HashMap, LinkedHashMap, TreeMap |
| *(add your notes files here as you create them)* | |

---

> ⭐ = High interview priority — revise these before every interview
>
> 💡 **Tip:** Don't try to learn everything at once.
> Finish Phase 1-4 first — that alone covers 70% of interview questions.