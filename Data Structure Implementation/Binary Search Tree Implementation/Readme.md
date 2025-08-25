# 🌲 Binary Search Tree (BST) Notes

---

## 📖 Introduction

A **Binary Search Tree (BST)** is a binary tree with a specific property: for every node, all values in its left subtree are less than the node's value, and all values in its right subtree are greater than the node's value. BSTs are widely used due to their efficient searching, insertion, and deletion operations.

---

## 🏷️ Properties

- **BST Property:**  
  For any node with value `N`:
  - All nodes in the left subtree have values `< N`
  - All nodes in the right subtree have values `> N`

- **No duplicate values** (in standard BSTs).

- **Average time complexity:**  
  - Search: O(log n)  
  - Insert: O(log n)  
  - Delete: O(log n)  
  _*Worst case: O(n) if the tree becomes skewed (like a linked list)._

---

## 🧩 Operations

### 1. Search

- Start from the root, compare the target value:
  - If equal, return the node.
  - If less, search in the left subtree.
  - If greater, search in the right subtree.

### 2. Insertion

- Recursively find the correct empty spot (left or right) and insert the new node.

### 3. Deletion

- Three cases:
  1. **Leaf Node:** Directly remove it.
  2. **One Child:** Replace node with its child.
  3. **Two Children:** Replace node with its inorder successor (smallest in the right subtree) or inorder predecessor (largest in the left subtree).

---

## 🛠️ Java Implementation

```java
class BSTNode {
    int data;
    BSTNode left, right;
    BSTNode(int data) {
        this.data = data;
        left = right = null;
    }
}

public class BST {
    BSTNode root;

    // Insert a value
    BSTNode insert(BSTNode node, int key) {
        if (node == null) return new BSTNode(key);
        if (key < node.data) node.left = insert(node.left, key);
        else if (key > node.data) node.right = insert(node.right, key);
        return node;
    }

    // Search a value
    boolean search(BSTNode node, int key) {
        if (node == null) return false;
        if (key == node.data) return true;
        return key < node.data ? search(node.left, key) : search(node.right, key);
    }

    // Inorder Traversal
    void inorder(BSTNode node) {
        if (node == null) return;
        inorder(node.left);
        System.out.print(node.data + " ");
        inorder(node.right);
    }

    // Delete a value
    BSTNode delete(BSTNode node, int key) {
        if (node == null) return null;
        if (key < node.data) node.left = delete(node.left, key);
        else if (key > node.data) node.right = delete(node.right, key);
        else {
            // Node with one or no child
            if (node.left == null) return node.right;
            else if (node.right == null) return node.left;
            // Node with two children
            node.data = minValue(node.right);
            node.right = delete(node.right, node.data);
        }
        return node;
    }

    // Helper to find min value
    int minValue(BSTNode node) {
        int minv = node.data;
        while (node.left != null) {
            minv = node.left.data;
            node = node.left;
        }
        return minv;
    }
}
```

---

## 🖼️ Visual Representation

```
      8
     / \
    3   10
   / \    \
  1   6    14
     / \   /
    4   7 13
```
**Inorder Traversal:** 1 3 4 6 7 8 10 13 14 (sorted order)

---

## 🌟 Applications & Use Cases

- Dynamic sorted data
- Implementation of sets and maps
- Range queries
- Searching, insertion, and deletion in O(log n) time (balanced BSTs)
- Used in databases, file systems, and more

---

## ⚠️ Drawbacks

- O(n) time in the worst case (unbalanced/skewed tree)
- Not suitable if frequent balancing is required (see AVL/Red-Black Trees)

---

## 💡 Common BST Interview Problems

1. **Validate if a Binary Tree is a BST**
2. **Find kth Smallest/Largest Element in BST**
3. **Lowest Common Ancestor in BST**
4. **BST to Sorted Doubly Linked List**
5. **Convert Sorted Array to BST**
6. **Find Floor and Ceil of a Value in BST**
7. **Delete a Node in BST**
8. **Find Inorder Successor/Predecessor**
9. **Range Sum in BST**
10. **Two Sum in BST**

---

> **Tip:** Practice BST operations and problems to master recursion and understand binary tree manipulations!
