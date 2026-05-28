# 📘 Java Collections: Sets & Maps — Complete Interview Guide

> A complete reference for `HashSet`, `LinkedHashSet`, `TreeSet`, `HashMap`, `LinkedHashMap`, `TreeMap` — internal workings, usage, and when to use what.

---

## 📑 Table of Contents

1. [Sets Overview](#sets-overview)
2. [HashSet](#1-hashset)
3. [LinkedHashSet](#2-linkedhashset)
4. [TreeSet](#3-treeset)
5. [Sets Comparison](#sets-comparison)
6. [Maps Overview](#maps-overview)
7. [HashMap](#4-hashmap)
8. [LinkedHashMap](#5-linkedhashmap)
9. [TreeMap](#6-treemap)
10. [Maps Comparison](#maps-comparison)
11. [Set vs Map — Key Difference](#set-vs-map)
12. [Common Interview Questions](#common-interview-questions)
13. [Quick Cheat Sheet](#quick-cheat-sheet)

---

## Sets Overview

A **Set** is a collection that:
- Does **NOT** allow duplicate elements
- Models the mathematical set abstraction

```
Java Set Hierarchy:

           <<interface>>
              Iterable
                 |
           <<interface>>
             Collection
                 |
           <<interface>>
               Set
              / | \
             /  |  \
        HashSet |  TreeSet
                |
         LinkedHashSet
```

---

## 1. HashSet

### What is it?
`HashSet` is backed by a **HashMap** internally. It stores elements in a **hash table** with no guaranteed order.

### Internal Working

```
How HashSet stores "apple", "banana", "cherry":

Step 1: Compute hashCode()
  "apple"  → hashCode() = 93029210  → bucket index = 93029210 % 16 = 10
  "banana" → hashCode() = -1396355602 → bucket index = 6
  "cherry" → hashCode() = -1582810614 → bucket index = 2

Step 2: Store in buckets (array of LinkedLists/Trees)

  Bucket Array (default capacity = 16):
  ┌─────┬──────────┐
  │  0  │  null    │
  │  1  │  null    │
  │  2  │ "cherry" │
  │  3  │  null    │
  │  4  │  null    │
  │  5  │  null    │
  │  6  │ "banana" │
  │  7  │  null    │
  │  8  │  null    │
  │  9  │  null    │
  │ 10  │ "apple"  │
  │ 11  │  null    │
  │ 12  │  null    │
  │ 13  │  null    │
  │ 14  │  null    │
  │ 15  │  null    │
  └─────┴──────────┘
```

### What happens on collision?

```
Two keys land in the same bucket → Collision!

Before Java 8:          After Java 8 (if bucket > 8 entries):
Linked List             Red-Black Tree (faster lookup)

Bucket[5]:              Bucket[5]:
"cat" → "bat" → null   "bat"
                       /    \
                    "cat"   "rat"

Why? LinkedList = O(n) lookup, Tree = O(log n)
```

### Duplicate Detection — How does add() work?

```
set.add("apple")  →  Already exists?
    │
    ▼
Compute hashCode("apple") → find bucket
    │
    ▼
Bucket empty?
  YES → add directly ✅
  NO  → check equals() with each element in bucket
          equals() = true?  → DUPLICATE, don't add ❌
          equals() = false? → Collision, add to chain ✅
```

### Key Parameters

| Parameter | Default | Meaning |
|---|---|---|
| Initial Capacity | 16 | Number of buckets |
| Load Factor | 0.75 | When to resize (75% full → double size) |
| Resize Trigger | capacity × load factor | 16 × 0.75 = 12 elements → resize to 32 |

### Code Usage

```java
import java.util.HashSet;

HashSet<String> set = new HashSet<>();

// Add
set.add("apple");
set.add("banana");
set.add("apple");   // duplicate → ignored

// Check
set.contains("apple");   // true
set.contains("grape");   // false

// Remove
set.remove("banana");

// Size
set.size();    // 1

// Iterate (ORDER NOT GUARANTEED)
for (String s : set) {
    System.out.println(s);
}

// Bulk operations
set.addAll(anotherSet);       // union
set.retainAll(anotherSet);    // intersection
set.removeAll(anotherSet);    // difference

// Convert from List (remove duplicates)
List<Integer> list = Arrays.asList(1, 2, 2, 3, 3);
Set<Integer> unique = new HashSet<>(list);   // {1, 2, 3}
```

### Time Complexity

| Operation | Average | Worst Case |
|---|---|---|
| `add()` | O(1) | O(n) |
| `remove()` | O(1) | O(n) |
| `contains()` | O(1) | O(n) |
| Iteration | O(n) | O(n) |

> Worst case is rare — happens with many hash collisions.

### When to use?
- Need fast O(1) add/search/remove
- Order doesn't matter
- Duplicate removal from a list
- Checking membership (visited nodes in graph, etc.)

---

## 2. LinkedHashSet

### What is it?
`LinkedHashSet` extends `HashSet` and maintains a **doubly linked list** running through all entries — preserving **insertion order**.

### Internal Working

```
LinkedHashSet adds a "prev" and "next" pointer to each bucket entry:

Insertion order: "apple" → "banana" → "cherry"

Hash Table (for O(1) lookup):
  bucket[10] → "apple"
  bucket[6]  → "banana"
  bucket[2]  → "cherry"

Doubly Linked List (for order):
  HEAD ↔ ["apple"] ↔ ["banana"] ↔ ["cherry"] ↔ TAIL

Iteration walks the linked list → always gives insertion order!
```

### Code Usage

```java
import java.util.LinkedHashSet;

LinkedHashSet<String> set = new LinkedHashSet<>();

set.add("banana");
set.add("apple");
set.add("cherry");
set.add("apple");   // duplicate → ignored

// Iterates in INSERTION ORDER
for (String s : set) {
    System.out.println(s);   // banana, apple, cherry
}
```

### Time Complexity

| Operation | Time |
|---|---|
| `add()` | O(1) |
| `remove()` | O(1) |
| `contains()` | O(1) |
| Iteration | O(n) |

### When to use?
- Need fast lookup (like HashSet) BUT also want insertion order
- Building an ordered unique list
- LRU Cache implementation
- Deduplication while preserving order

---

## 3. TreeSet

### What is it?
`TreeSet` is backed by a **Red-Black Tree** (a self-balancing BST). Elements are stored in **sorted (natural) order**.

### Internal Working

```
TreeSet stores: 5, 3, 7, 1, 4

Red-Black Tree:
           5 (Black)
          / \
       3 (Red) 7 (Red)
      / \
  1(Black) 4(Black)

Rules of Red-Black Tree:
  1. Every node is Red or Black
  2. Root is always Black
  3. No two adjacent Red nodes
  4. Every path from root to null has same number of Black nodes

Why? These rules keep the tree BALANCED → guarantees O(log n) operations
```

### Code Usage

```java
import java.util.TreeSet;

TreeSet<Integer> set = new TreeSet<>();

set.add(5);
set.add(3);
set.add(7);
set.add(1);
set.add(3);   // duplicate → ignored

// Iterates in SORTED ORDER
for (int n : set) {
    System.out.print(n + " ");   // 1 3 5 7
}

// Navigation methods (TreeSet exclusive!)
set.first();           // 1 — smallest
set.last();            // 7 — largest
set.floor(4);          // 3 — largest element ≤ 4
set.ceiling(4);        // 5 — smallest element ≥ 4
set.lower(5);          // 3 — largest element strictly < 5
set.higher(5);         // 7 — smallest element strictly > 5

set.headSet(5);        // [1, 3]      — elements < 5
set.tailSet(5);        // [5, 7]      — elements ≥ 5
set.subSet(3, 7);      // [3, 5]      — elements from 3 (inclusive) to 7 (exclusive)

// Reverse order
set.descendingSet();   // [7, 5, 3, 1]
```

### Custom Sorting with Comparator

```java
// Sort strings by length
TreeSet<String> byLength = new TreeSet<>(Comparator.comparingInt(String::length));
byLength.add("banana");
byLength.add("fig");
byLength.add("apple");

// Iteration: fig, apple, banana
```

### Time Complexity

| Operation | Time |
|---|---|
| `add()` | O(log n) |
| `remove()` | O(log n) |
| `contains()` | O(log n) |
| `first()` / `last()` | O(log n) |
| Iteration | O(n) |

### When to use?
- Need elements in sorted order
- Need range queries (`headSet`, `subSet`, `tailSet`)
- Need floor/ceiling navigation
- Priority-based processing without a PriorityQueue

---

## Sets Comparison

```
Feature Comparison:

┌─────────────────┬───────────┬────────────────┬──────────┐
│    Feature      │  HashSet  │ LinkedHashSet  │ TreeSet  │
├─────────────────┼───────────┼────────────────┼──────────┤
│ Order           │   None    │  Insertion     │  Sorted  │
│ Null elements   │   1 null  │  1 null        │  ❌ No   │
│ add/remove      │   O(1)    │  O(1)          │  O(log n)│
│ contains        │   O(1)    │  O(1)          │  O(log n)│
│ Backed by       │  HashMap  │ LinkedHashMap  │ Red-Black│
│                 │           │                │  Tree    │
│ Navigation      │    ❌     │    ❌          │  ✅      │
│ Thread-safe     │    ❌     │    ❌          │  ❌      │
└─────────────────┴───────────┴────────────────┴──────────┘
```

**Decision Tree:**
```
Need a Set?
    │
    ├── Need SORTED order? ──→ TreeSet
    │
    ├── Need INSERTION order? ──→ LinkedHashSet
    │
    └── Don't care about order? ──→ HashSet (fastest)
```

---

## Maps Overview

A **Map** stores **key-value pairs**. Keys are unique; values can repeat.

```
Java Map Hierarchy:

           <<interface>>
               Map
              / | \
             /  |  \
        HashMap |  TreeMap
                |
         LinkedHashMap
```

---

## 4. HashMap

### What is it?
`HashMap` stores key-value pairs in a **hash table** (array of buckets). No guaranteed order.

### Internal Working

```
HashMap internals (same hashing as HashSet, but stores key + value):

put("name", "Alice")
put("age", "25")
put("city", "Delhi")

  Bucket Array:
  ┌──────┬─────────────────────────────┐
  │  0   │  null                       │
  │  1   │  null                       │
  │  2   │  "city" → "Delhi"           │
  │  3   │  null                       │
  │  4   │  "name" → "Alice"           │
  │  5   │  null                       │
  │  6   │  "age"  → "25"              │
  │ ...  │  ...                        │
  └──────┴─────────────────────────────┘

Each bucket node contains: [hash | key | value | next]
```

### Collision in HashMap

```
Two different keys → same bucket → Collision!

Bucket[4]:  "name" → "Alice"  →  "mane" → "Bob"  (linked list)

After 8 entries in a bucket → converts to Red-Black Tree
(same as HashSet, since HashSet IS a HashMap with dummy values)
```

### Code Usage

```java
import java.util.HashMap;

HashMap<String, Integer> map = new HashMap<>();

// Put / Update
map.put("alice", 90);
map.put("bob", 85);
map.put("alice", 95);    // updates existing key

// Get
map.get("alice");        // 95
map.get("charlie");      // null

// Safe get with default
map.getOrDefault("charlie", 0);   // 0

// Check
map.containsKey("bob");      // true
map.containsValue(95);       // true

// Remove
map.remove("bob");
map.remove("alice", 90);     // removes only if value matches

// Size
map.size();    // 1

// Iterate — 3 ways
// 1. EntrySet (most common, most efficient)
for (Map.Entry<String, Integer> entry : map.entrySet()) {
    System.out.println(entry.getKey() + " → " + entry.getValue());
}

// 2. KeySet
for (String key : map.keySet()) {
    System.out.println(key + " → " + map.get(key));
}

// 3. Values only
for (int val : map.values()) {
    System.out.println(val);
}

// Useful methods
map.putIfAbsent("dave", 70);           // only puts if key absent
map.merge("alice", 5, Integer::sum);   // alice = 95 + 5 = 100
map.computeIfAbsent("eve", k -> 60);   // compute value if key absent

// Frequency counter pattern (very common!)
String[] words = {"a", "b", "a", "c", "b", "a"};
HashMap<String, Integer> freq = new HashMap<>();
for (String w : words) {
    freq.put(w, freq.getOrDefault(w, 0) + 1);
}
// {a=3, b=2, c=1}
```

### Time Complexity

| Operation | Average | Worst Case |
|---|---|---|
| `put()` | O(1) | O(n) |
| `get()` | O(1) | O(n) |
| `remove()` | O(1) | O(n) |
| `containsKey()` | O(1) | O(n) |

### When to use?
- Frequency counting
- Caching/memoization
- Grouping elements by key
- Any key-value lookup where order doesn't matter

---

## 5. LinkedHashMap

### What is it?
`LinkedHashMap` extends `HashMap` and maintains a **doubly linked list** to preserve **insertion order** (or access order if configured).

### Internal Working

```
LinkedHashMap — HashMap + Doubly Linked List:

put("c", 3)  →  bucket[2]
put("a", 1)  →  bucket[4]
put("b", 2)  →  bucket[6]

Hash table (for O(1) lookup):
  bucket[2] → ("c", 3)
  bucket[4] → ("a", 1)
  bucket[6] → ("b", 2)

Linked List (preserves order):
  HEAD ↔ ("c",3) ↔ ("a",1) ↔ ("b",2) ↔ TAIL

Iteration gives: c=3, a=1, b=2  (insertion order!)
```

### Access Order Mode — LRU Cache!

```java
// accessOrder = true → most recently accessed goes to END
LinkedHashMap<String, Integer> lru = new LinkedHashMap<>(16, 0.75f, true);

lru.put("a", 1);
lru.put("b", 2);
lru.put("c", 3);

lru.get("a");   // access "a" → moves to end

// Order now: b, c, a  (a was most recently accessed)
```

### LRU Cache Implementation

```java
class LRUCache<K, V> extends LinkedHashMap<K, V> {
    private final int capacity;

    public LRUCache(int capacity) {
        super(capacity, 0.75f, true);   // accessOrder = true
        this.capacity = capacity;
    }

    @Override
    protected boolean removeEldestEntry(Map.Entry<K, V> eldest) {
        return size() > capacity;       // evict least recently used
    }
}

LRUCache<Integer, String> cache = new LRUCache<>(3);
cache.put(1, "one");
cache.put(2, "two");
cache.put(3, "three");
cache.get(1);           // access 1 → moves to end
cache.put(4, "four");   // evicts LRU → removes 2
// Cache: {3=three, 1=one, 4=four}
```

### When to use?
- Need HashMap performance + insertion order
- LRU Cache (with accessOrder = true)
- Processing entries in the order they were added

---

## 6. TreeMap

### What is it?
`TreeMap` is backed by a **Red-Black Tree**. Keys are stored in **sorted (natural) order**.

### Internal Working

```
TreeMap stores: put(5,"e"), put(3,"c"), put(7,"g"), put(1,"a")

Red-Black Tree (sorted by KEY):
             5,"e" (Black)
            /       \
       3,"c"(Red)  7,"g"(Red)
       /
   1,"a"(Black)

Inorder traversal → 1,3,5,7 → always sorted!
```

### Code Usage

```java
import java.util.TreeMap;

TreeMap<Integer, String> map = new TreeMap<>();

map.put(5, "five");
map.put(3, "three");
map.put(7, "seven");
map.put(1, "one");

// Iterates in SORTED KEY ORDER
for (Map.Entry<Integer, String> e : map.entrySet()) {
    System.out.println(e.getKey() + " → " + e.getValue());
}
// 1→one, 3→three, 5→five, 7→seven

// Navigation methods (TreeMap exclusive!)
map.firstKey();          // 1
map.lastKey();           // 7
map.floorKey(4);         // 3 — largest key ≤ 4
map.ceilingKey(4);       // 5 — smallest key ≥ 4
map.lowerKey(5);         // 3 — largest key strictly < 5
map.higherKey(5);        // 7 — smallest key strictly > 5

map.headMap(5);          // {1=one, 3=three}        — keys < 5
map.tailMap(5);          // {5=five, 7=seven}       — keys ≥ 5
map.subMap(3, 7);        // {3=three, 5=five}       — keys [3, 7)

map.firstEntry();        // 1=one
map.lastEntry();         // 7=seven
map.pollFirstEntry();    // removes and returns 1=one
map.pollLastEntry();     // removes and returns 7=seven

// Reverse order
map.descendingMap();     // {7=seven, 5=five, 3=three, 1=one}
```

### Custom Comparator

```java
// Sort by reverse order
TreeMap<Integer, String> reverseMap = new TreeMap<>(Comparator.reverseOrder());
reverseMap.put(1, "one");
reverseMap.put(3, "three");
reverseMap.put(2, "two");
// Iteration: 3→three, 2→two, 1→one
```

### Time Complexity

| Operation | Time |
|---|---|
| `put()` | O(log n) |
| `get()` | O(log n) |
| `remove()` | O(log n) |
| `firstKey()` / `lastKey()` | O(log n) |
| Iteration | O(n) |

### When to use?
- Need sorted key order
- Range queries (all keys between X and Y)
- Floor/ceiling lookups
- Finding closest key to a value

---

## Maps Comparison

```
Feature Comparison:

┌─────────────────┬───────────┬────────────────┬──────────┐
│    Feature      │  HashMap  │ LinkedHashMap  │ TreeMap  │
├─────────────────┼───────────┼────────────────┼──────────┤
│ Order           │   None    │  Insertion     │  Sorted  │
│ Null Keys       │  1 null   │  1 null        │  ❌ No   │
│ Null Values     │  ✅ Yes   │  ✅ Yes        │  ✅ Yes  │
│ put/get         │   O(1)    │  O(1)          │ O(log n) │
│ Backed by       │  Hash tbl │  Hash tbl +    │ Red-Black│
│                 │           │  LinkedList    │  Tree    │
│ Navigation      │    ❌     │    ❌          │  ✅      │
│ Thread-safe     │    ❌     │    ❌          │  ❌      │
└─────────────────┴───────────┴────────────────┴──────────┘
```

**Decision Tree:**
```
Need a Map?
    │
    ├── Need SORTED keys? ──→ TreeMap
    │
    ├── Need INSERTION order? ──→ LinkedHashMap
    │
    ├── Need LRU Cache? ──→ LinkedHashMap (accessOrder=true)
    │
    └── Don't care about order? ──→ HashMap (fastest)
```

---

## Set vs Map

```
┌──────────────────────────────────────────────────────┐
│                    SET                               │
│                                                      │
│  { "apple", "banana", "cherry" }                     │
│                                                      │
│  Stores: UNIQUE ELEMENTS only                        │
│  Think: A bag where every item is unique             │
└──────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────┐
│                    MAP                               │
│                                                      │
│  { "name"→"Alice", "age"→25, "city"→"Delhi" }        │
│                                                      │
│  Stores: KEY-VALUE PAIRS (unique keys)               │
│  Think: A dictionary with unique words & definitions │
└──────────────────────────────────────────────────────┘

Fun fact: HashSet IS a HashMap internally!
  → HashSet stores keys with a dummy PRESENT object as value
  → set.add("apple") = map.put("apple", PRESENT)
```

---

## Common Interview Questions

### Q1. How does HashMap handle null keys?
```java
// HashMap allows ONE null key
map.put(null, "value");   // stores in bucket[0]
map.get(null);            // "value" ✅

// TreeMap does NOT allow null keys (can't compare null)
// Throws NullPointerException
```

---

### Q2. What is the difference between HashMap and Hashtable?
```
HashMap:
  - Not thread-safe
  - Allows 1 null key, multiple null values
  - Faster (no synchronization overhead)
  - Use in single-threaded code

Hashtable:
  - Thread-safe (synchronized methods)
  - No null keys or values
  - Slower
  - Legacy class — prefer ConcurrentHashMap for thread safety
```

---

### Q3. What happens when two objects have the same hashCode?
```
Collision! Java handles it:
  1. Both go into the same bucket
  2. Java checks equals() to see if they're truly equal
  3. If equals() → true: it's a duplicate, don't add
  4. If equals() → false: add to the bucket's chain (LinkedList or Tree)

⚠️ Contract: if a.equals(b) → a.hashCode() == b.hashCode() (MUST)
              if a.hashCode() == b.hashCode() → a.equals(b) MAY or MAY NOT be true
```

---

### Q4. Why override both hashCode() and equals()?
```java
class Person {
    String name;
    int age;

    // Without overriding: default uses memory address
    // Two "same" persons would be treated as different!

    @Override
    public boolean equals(Object o) {
        Person p = (Person) o;
        return name.equals(p.name) && age == p.age;
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, age);   // MUST override both!
    }
}

// If you only override equals() but not hashCode():
// Two equal persons may land in different buckets → HashMap breaks!
```

---

### Q5. When does HashMap resize?
```
Initial capacity = 16, Load factor = 0.75

Resize triggers when: size > capacity × loadFactor
                             > 16 × 0.75
                             > 12 elements

On resize:
  1. New array created with double capacity (16 → 32)
  2. ALL existing entries are rehashed and redistributed
  3. This is expensive! Pre-size if you know the count:

new HashMap<>(100);        // initial capacity hint
new HashMap<>(100, 0.9f);  // also custom load factor
```

---

### Q6. What is ConcurrentHashMap? (Bonus)
```java
// Thread-safe version of HashMap
// Does NOT lock the whole map — locks individual segments

import java.util.concurrent.ConcurrentHashMap;

ConcurrentHashMap<String, Integer> map = new ConcurrentHashMap<>();
map.put("a", 1);
map.get("a");

// Use when: multiple threads read/write the map simultaneously
// Faster than Hashtable, safer than HashMap for concurrent use
```

---

### Q7. HashMap vs HashSet internal relationship?
```java
// HashSet source code (simplified):
public class HashSet<E> {
    private HashMap<E, Object> map;           // backed by HashMap!
    private static final Object PRESENT = new Object();  // dummy value

    public boolean add(E e) {
        return map.put(e, PRESENT) == null;   // key = element, value = dummy
    }

    public boolean contains(Object o) {
        return map.containsKey(o);
    }
}
```

---

## Quick Cheat Sheet

```
SETS — When to use:

  HashSet        → fast lookup, no order needed       → O(1) ops
  LinkedHashSet  → fast lookup + insertion order      → O(1) ops
  TreeSet        → sorted order, range queries        → O(log n) ops

MAPS — When to use:

  HashMap        → fast key-value, no order           → O(1) ops
  LinkedHashMap  → fast lookup + insertion order      → O(1) ops
                   also for LRU Cache
  TreeMap        → sorted keys, range/floor/ceiling   → O(log n) ops

INTERNAL BACKING:

  HashSet        → HashMap (keys only, dummy value)
  LinkedHashSet  → LinkedHashMap
  TreeSet        → TreeMap (keys only, dummy value)
  HashMap        → array of buckets (LinkedList → Tree on overflow)
  LinkedHashMap  → HashMap + doubly linked list
  TreeMap        → Red-Black Tree

NULL RULES:

  HashSet        → 1 null element allowed
  LinkedHashSet  → 1 null element allowed
  TreeSet        → ❌ no null
  HashMap        → 1 null key, many null values
  LinkedHashMap  → 1 null key, many null values
  TreeMap        → ❌ no null key, null values ok

THREAD SAFETY:

  None of the above are thread-safe!
  Use: Collections.synchronizedMap(map)
  Or:  ConcurrentHashMap (preferred for maps)
  Or:  CopyOnWriteArraySet (preferred for sets)
```

---

> 💡 **Golden Rule for Interviews:**
> - Default to **HashMap / HashSet** (fastest)
> - Need order? → **LinkedHashMap / LinkedHashSet**
> - Need sorting or range queries? → **TreeMap / TreeSet**
> - Need thread safety? → **ConcurrentHashMap**
> - Always remember: **equals() + hashCode()** contract!