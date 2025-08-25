# 🗺️ HashMap Notes

---

## 📖 Introduction

A **HashMap** (also called Hash Table or Dictionary) is a data structure that stores key-value pairs. It provides very fast insertion, deletion, and lookup (average-case O(1) time) by using a hash function to map keys to buckets.

---

## 🏷️ Key Concepts

- **Key-Value Pair:** Each entry has a unique key and a value.
- **Hash Function:** Converts a key to an integer (hash code), which determines the index (bucket) where the entry is stored.
- **Bucket:** A location in the underlying array; may contain one or more entries (for collision handling).
- **Collision:** When two keys hash to the same bucket; handled by chaining (linked list) or open addressing (probing).
- **Load Factor:** Ratio of number of entries to the number of buckets. High load factor triggers resizing (rehashing).
- **Rehashing:** Expanding array size and re-inserting all entries when load factor exceeds a threshold.

---

## 🧩 HashMap Implementation Approaches

### 1. Separate Chaining (with Linked List)

```java
class Entry<K, V> {
    K key;
    V value;
    Entry<K, V> next;
    Entry(K key, V value) {
        this.key = key;
        this.value = value;
        this.next = null;
    }
}

class MyHashMap<K, V> {
    private int SIZE = 16;
    private Entry<K, V>[] table;

    public MyHashMap() {
        table = new Entry[SIZE];
    }

    private int hash(K key) {
        return key == null ? 0 : Math.abs(key.hashCode() % SIZE);
    }

    public void put(K key, V value) {
        int idx = hash(key);
        Entry<K, V> head = table[idx];
        Entry<K, V> curr = head;
        while (curr != null) {
            if ((key == null && curr.key == null) || (key != null && key.equals(curr.key))) {
                curr.value = value; // Update existing
                return;
            }
            curr = curr.next;
        }
        Entry<K, V> newEntry = new Entry<>(key, value);
        newEntry.next = head;
        table[idx] = newEntry;
    }

    public V get(K key) {
        int idx = hash(key);
        Entry<K, V> curr = table[idx];
        while (curr != null) {
            if ((key == null && curr.key == null) || (key != null && key.equals(curr.key))) {
                return curr.value;
            }
            curr = curr.next;
        }
        return null;
    }

    public void remove(K key) {
        int idx = hash(key);
        Entry<K, V> curr = table[idx], prev = null;
        while (curr != null) {
            if ((key == null && curr.key == null) || (key != null && key.equals(curr.key))) {
                if (prev == null) table[idx] = curr.next;
                else prev.next = curr.next;
                return;
            }
            prev = curr;
            curr = curr.next;
        }
    }
}
```

---

### 2. Using Java Collections Framework

```java
import java.util.HashMap;

HashMap<String, Integer> map = new HashMap<>();
map.put("apple", 2);
map.put("banana", 5);
System.out.println(map.get("apple")); // 2
map.remove("banana");
System.out.println(map.containsKey("apple")); // true
```

---

## 🖼️ Visual Representation

```
Index:    0      1      2      3      4
        ------ ------ ------ ------ ------
        [   ]  [   ]  [   ]  [   ]  [   ]
                |             |
                v             v
             [key1]        [key2]
               |             |
             [key3]         null
               |
              null
```
_Buckets are linked lists of entries (chaining)._

---

## 🌟 Applications & Use Cases

- Database indexing
- Caching
- Symbol tables in compilers/interpreters
- Counting frequencies (e.g., in strings, arrays)
- Implementing sets and dictionaries

---

## ⚠️ Important Points & Pitfalls

- Good hash function minimizes collisions.
- Keys must be immutable and properly implement `hashCode()` and `equals()`.
- Java's `HashMap` is **not synchronized** (not thread-safe). Use `ConcurrentHashMap` for concurrency.
- High load factor leads to performance degradation.
- Order is not guaranteed in `HashMap`. Use `LinkedHashMap` if order matters.

---

## 💡 Common HashMap Interview Problems

1. **Two Sum Problem**
2. **Subarrays with Given Sum/Frequency**
3. **Group Anagrams**
4. **Longest Consecutive Sequence**
5. **First Non-Repeating Character**
6. **Clone a Graph**
7. **LRU Cache**
8. **Find All Duplicates in Array**
9. **Word Pattern / Isomorphic Strings**
10. **Top K Frequent Elements**

---

> **Tip:** Practice using both custom and built-in hash maps, and always check key hashability and proper usage of `equals()` and `hashCode()` for custom objects!
