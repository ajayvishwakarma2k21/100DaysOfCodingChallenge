# 🌳 Binary Tree Notes

---

## 📖 Introduction

A **Binary Tree** is a hierarchical data structure in which each node has at most two children, referred to as the left child and the right child. Binary trees are fundamental in computer science and serve as the basis for more advanced data structures like binary search trees, heaps, and syntax trees.

---

## 🏷️ Basic Terminologies

- **Node**: The basic unit containing data and links to child nodes.
- **Root**: The topmost node of the tree.
- **Leaf Node**: A node with no children.
- **Parent/Child**: Relationship between nodes directly connected.
- **Subtree**: A tree formed by a node and its descendants.
- **Height**: Number of edges on the longest path from a node to a leaf.
- **Depth**: Number of edges from the root to a node.
- **Level**: Number of edges from the root node (root is at level 0).

---

## 🧩 Types of Binary Trees

1. **Full Binary Tree**  
   Every node has 0 or 2 children.

2. **Perfect Binary Tree**  
   All internal nodes have 2 children, and all leaves are at the same level.

3. **Complete Binary Tree**  
   All levels except possibly the last are completely filled, and all nodes are as far left as possible.

4. **Balanced Binary Tree**  
   Height of left and right subtrees of every node differ by at most 1.

5. **Degenerate (Skewed) Tree**  
   Each parent node has only one child (resembles a linked list).

---

## 🌟 Properties

- A binary tree with `n` nodes has exactly `n-1` edges.
- The maximum number of nodes at level `l` = 2^l.
- The maximum number of nodes in a binary tree of height `h` = 2^(h+1) - 1.
- In a perfect binary tree, number of leaf nodes = (n + 1)/2.

---

## ⚡ Traversal Techniques

### 1. Inorder (Left, Root, Right)
- Used in BSTs to get sorted order.
- Example: `inorder(root.left); visit(root); inorder(root.right);`

### 2. Preorder (Root, Left, Right)
- Used to create a copy of the tree.

### 3. Postorder (Left, Right, Root)
- Used to delete the tree.

### 4. Level Order (Breadth-First)
- Visit all nodes level by level, often using a queue.

---

## 🛠️ Implementation in Java

```java
class TreeNode {
    int data;
    TreeNode left, right;

    TreeNode(int data) {
        this.data = data;
        left = right = null;
    }
}

public class BinaryTree {
    TreeNode root;

    // Inorder Traversal
    void inorder(TreeNode node) {
        if (node == null) return;
        inorder(node.left);
        System.out.print(node.data + " ");
        inorder(node.right);
    }

    // Preorder Traversal
    void preorder(TreeNode node) {
        if (node == null) return;
        System.out.print(node.data + " ");
        preorder(node.left);
        preorder(node.right);
    }

    // Postorder Traversal
    void postorder(TreeNode node) {
        if (node == null) return;
        postorder(node.left);
        postorder(node.right);
        System.out.print(node.data + " ");
    }
}
```

---

## 🖼️ Visual Representation

```
        1
       / \
      2   3
     / \   \
    4   5   6
```
- Inorder: 4 2 5 1 3 6
- Preorder: 1 2 4 5 3 6
- Postorder: 4 5 2 6 3 1

---

## 💡 Common Interview Problems on Binary Trees

1. **Maximum Depth of Binary Tree**  
2. **Check if Binary Tree is Balanced**
3. **Diameter of Binary Tree**
4. **Invert (Mirror) Binary Tree**
5. **Level Order Traversal**
6. **Zigzag Level Order Traversal**
7. **Lowest Common Ancestor**
8. **Check if Two Trees are Identical**
9. **Serialize and Deserialize Binary Tree**
10. **Path Sum Problems**

---

> **Tip:** Practice tree problems regularly to master recursion and improve problem-solving skills!
