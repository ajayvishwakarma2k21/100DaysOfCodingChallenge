# 🌲 Trie (Prefix Tree) Notes

---

## 📖 Introduction

A **Trie**, also known as a **Prefix Tree** or **Digital Tree**, is a tree-like data structure used to efficiently store and retrieve keys in a dataset of strings. It is especially useful for autocomplete, spell checking, and prefix-based search operations.

---

## 🏷️ Key Concepts

- **Node:** Each node represents a character of a string.
- **Root:** The topmost node (often empty or null character).
- **Children:** Each node may have multiple child nodes (one for each possible character).
- **End of Word Flag:** Marks if a node represents the end of a valid word/key.
- **Alphabet Size:** For lowercase English, typically 26 children per node.

---

## 🛠️ Trie Implementation in Java

```java
class TrieNode {
    TrieNode[] children = new TrieNode[26]; // For a-z
    boolean isEndOfWord;

    TrieNode() {
        isEndOfWord = false;
    }
}

public class Trie {
    private TrieNode root;

    public Trie() {
        root = new TrieNode();
    }

    // Insert a word into the trie
    public void insert(String word) {
        TrieNode node = root;
        for (char ch : word.toCharArray()) {
            int idx = ch - 'a';
            if (node.children[idx] == null) node.children[idx] = new TrieNode();
            node = node.children[idx];
        }
        node.isEndOfWord = true;
    }

    // Search for a word in the trie
    public boolean search(String word) {
        TrieNode node = root;
        for (char ch : word.toCharArray()) {
            int idx = ch - 'a';
            if (node.children[idx] == null) return false;
            node = node.children[idx];
        }
        return node.isEndOfWord;
    }

    // Check if there is any word in the trie that starts with the given prefix
    public boolean startsWith(String prefix) {
        TrieNode node = root;
        for (char ch : prefix.toCharArray()) {
            int idx = ch - 'a';
            if (node.children[idx] == null) return false;
            node = node.children[idx];
        }
        return true;
    }
}
```

---

## 🖼️ Visual Representation

Suppose we insert `["to", "tea", "ten", "inn"]`:

```
          (root)
         /   |     \
       i     t      ...
       |    / \
       n   e   o
       |   |    \
       n   a     (end)
      (end)(end) (end)
```
- Words end at nodes marked as (end).

---

## 🌟 Applications & Use Cases

- **Autocomplete/Spell Checker**
- **Prefix-based search**
- **IP Routing (Longest Prefix Matching)**
- **Word Games and Puzzles**
- **Dictionary Implementations**

---

## ⚡ Trie Characteristics

- **Time Complexity:**
  - Insert: O(L), Search: O(L), Prefix: O(L) (`L` = length of word/prefix)
- **Space Complexity:** High, especially for large alphabets or sparse data (can be optimized with hash maps or compressed tries).

---

## ⚠️ Important Points

- For large character sets, use `Map<Character, TrieNode>` for children to save space.
- Supports fast search, insert, and prefix queries.
- Variants: Suffix Trie, Compressed Trie (Radix Tree), Ternary Search Tree.

---

## 💡 Common Trie Interview Problems

1. **Implement Trie (Insert, Search, StartsWith)**
2. **Word Search II (Find Words in Grid)**
3. **Longest Word in Dictionary**
4. **Replace Words (Prefix Replacement)**
5. **Design Add and Search Words Data Structure**
6. **Maximum XOR of Two Numbers in an Array**
7. **Count Words with Given Prefix**
8. **Palindrome Pairs**
9. **Auto-complete System**
10. **Unique Prefix for Every Word**

---

> **Tip:** Tries are invaluable for string and prefix problems. Know how to implement and optimize them for coding interviews!
