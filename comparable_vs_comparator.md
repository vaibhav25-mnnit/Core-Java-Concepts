# Java Sorting Cheat Sheet: Comparable vs. Comparator

A quick-reference guide to master the core differences between `Comparable` and `Comparator` for interviews and development.

---

## 💡 The Core Difference

The names sound almost identical, but they have **no inheritance relationship**. They are two completely separate, independent interfaces.

* **`Comparable`** defines **Natural Ordering** (What the object *is*). The class sorts *itself*.
* **`Comparator`** defines **Custom/External Ordering** (How you want to sort it *now*). An *outside tool* sorts the collection.

---

## 🔍 Key Comparison Matrix

| Feature | `Comparable` | `Comparator` |
| :--- | :--- | :--- |
| **Package** | `java.lang` (No import needed) | `java.util` (Requires import) |
| **Method** | `compareTo(T o)` | `compare(T o1, T o2)` |
| **Arguments** | Takes **one** argument (`this` vs `other`) | Takes **two** arguments (`obj1` vs `obj2`) |
| **Source Code** | **Must** modify the original class code. | **No** modification needed to the original class. |
| **Flexibility** | Exactly **one** default sorting sequence. | **Unlimited** custom sorting strategies. |
| **Usage** | `Collections.sort(list);` | `Collections.sort(list, comparator);` |

---

## ⚔️ Detailed Interview Comparison

| Feature | `Comparable` | `Comparator` |
| :--- | :--- | :--- |
| **Package** | `java.lang` (No import needed) | `java.util` (Requires import) |
| **Method** | `compareTo(Object o)` | `compare(Object o1, Object o2)` |
| **Parameters** | Takes **one** parameter (compares `this` to `other`) | Takes **two** parameters (compares two external objects) |
| **Class Modification** | **Must** alter the actual class source code. | **No** modification needed to the actual class. |
| **Flexibility** | Provides only **one** default sorting sequence. | Provides **multiple** sorting sequences (separate logic for separate fields). |
| **Typical Use Case** | Used for standard data types or defining the absolute default behavior of a domain object. | Used when you need custom sorting, conditional sorting, or when working with third-party classes. |

---

## 💻 Code Blueprints

### 1. Comparable (Default Inherent Sorting)
Use this to define the absolute default way an object should be sorted (e.g., by ID).

```java
import java.lang.Comparable;

public class Employee implements Comparable<Employee> {
    private int id;
    private String name;

    public Employee(int id, String name) {
        this.id = id;
        this.name = name;
    }

    // "Compare me (this) to that other object"
    @Override
    public int compareTo(Employee other) {
        return Integer.compare(this.id, other.id); // Ascending by ID
    }
}
