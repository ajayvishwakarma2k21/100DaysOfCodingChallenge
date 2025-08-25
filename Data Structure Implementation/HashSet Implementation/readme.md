# 🗂️ HashSet Notes

---

## 📖 Introduction

A **HashSet** is a data structure that stores unique elements in no particular order. It is implemented using a hash table and provides constant time (O(1) average) for add, remove, and contains operations. In Java, `HashSet` is part of the Java Collections Framework and internally uses a `HashMap`.

---

## 🏷️ Key Concepts

- **No Duplicates:** Each element is unique; duplicates are ignored.
- **Unordered:** There is no guarantee of order (insertion or sorted) in a `HashSet`.
- **Underlying Structure:** Usually backed by a hash table (hashing).
- **Null Allowed:** A single `null` element is permitted.
- **Performance:** O(1) average time for add, remove, and contains.

---

## 🧩 HashSet Implementation Approach

### 1. Custom Implementation Using Hash Table (Separate Chaining)

```java
class Node {
    int key;
    Node next;
    Node(int key) { this.key = key; }
}

class MyHashSet {
    private int SIZE = 1000;
    private Node[] buckets = new Node[SIZE];

    private int hash(int key) {
        return Math.abs(key) % SIZE;
    }

    public void add(int key) {
        int idx = hash(key);
        Node curr = buckets[idx];
        while (curr != null) {
            if (curr.key == key) return; // already present
            curr = curr.next;
        }
        Node node = new Node(key);
        node.next = buckets[idx];
        buckets[idx] = node;
    }

    public void remove(int key) {
        int idx = hash(key);
        Node curr = buckets[idx], prev = null;
        while (curr != null) {
            if (curr.key == key) {
                if (prev == null) buckets[idx] = curr.next;
                else prev.next = curr.next;
                return;
            }
            prev = curr;
            curr = curr.next;
        }
    }

    public boolean contains(int key) {
        int idx = hash(key);
        Node curr = buckets[idx];
        while (curr != null) {
            if (curr.key == key) return true;
            curr = curr.next;
        }
        return false;
    }
}
```

---

### 2. Using Java Collections Framework

```java
import java.util.HashSet;

HashSet<String> set = new HashSet<>();
set.add("apple");
set.add("banana");
set.add("apple"); // Duplicate, will not be added
System.out.println(set.contains("banana")); // true
set.remove("banana");
System.out.println(set); // [apple]
```

---

## 🖼️ Visual Representation

```
Index:   0      1      2      3      4    ...
        ------ ------ ------ ------ ------
        [   ]  [cat]  [   ]  [dog] [   ]
```
_Elements are distributed in buckets based on their hash codes. No duplicates._

---

## 🌟 Applications & Use Cases

- Removing duplicates from a collection
- Membership testing (is an item present?)
- Finding intersection, union, or difference between sets
- Fast lookups in algorithms (like Two Sum, Longest Consecutive Sequence, etc.)
- Unique word or character detection

---

## ⚠️ Important Points

- Good hashCode and equals methods are crucial for user-defined objects.
- Not thread-safe; use `Collections.synchronizedSet` or `ConcurrentHashMap.newKeySet()` for concurrency.
- Use `LinkedHashSet` if you need insertion order, and `TreeSet` for sorted order.

---

## 💡 Common HashSet Interview Problems

1. **Remove Duplicates from Array/List**
2. **Check If Array Contains Duplicates**
3. **Longest Consecutive Sequence**
4. **Intersection/Union of Two Arrays**
5. **Happy Number**
6. **Find Pair with Given Sum**
7. **First Repeating/Non-Repeating Character**
8. **Detect Cycle in a Linked List**
9. **Isomorphic Strings**
10. **Word Break Problem**

---

> **Tip:** Use a `HashSet` whenever you need fast existence checks or uniqueness in a collection!
