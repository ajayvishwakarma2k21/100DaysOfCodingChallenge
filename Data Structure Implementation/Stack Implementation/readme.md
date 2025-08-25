# 📚 Stack Notes

---

## 📖 Introduction

A **Stack** is a linear data structure that follows the Last-In-First-Out (LIFO) principle. The element added last is the first one to be removed. Think of a stack like a pile of plates—add (push) to the top and remove (pop) from the top.

---

## 🏷️ Basic Operations

- **Push:** Add an element to the top of the stack.
- **Pop:** Remove and return the top element.
- **Peek/Top:** View the top element without removing it.
- **isEmpty:** Check if the stack is empty.
- **Size:** Return the number of elements in the stack.

---

## 🧩 Stack Implementation Methods

### 1. Using Arrays

- Fixed size (static).
- Easy and fast, but limited by array size.

```java
class StackArray {
    private int maxSize;
    private int[] stack;
    private int top;

    public StackArray(int size) {
        maxSize = size;
        stack = new int[maxSize];
        top = -1;
    }

    public void push(int x) {
        if (top == maxSize - 1) throw new StackOverflowError("Stack is full");
        stack[++top] = x;
    }

    public int pop() {
        if (top == -1) throw new RuntimeException("Stack is empty");
        return stack[top--];
    }

    public int peek() {
        if (top == -1) throw new RuntimeException("Stack is empty");
        return stack[top];
    }

    public boolean isEmpty() {
        return top == -1;
    }

    public int size() {
        return top + 1;
    }
}
```

---

### 2. Using Linked List

- Dynamic size (no overflow unless out of memory).
- Each node holds data and a pointer to the next node.

```java
class Node {
    int data;
    Node next;
    Node(int data) { this.data = data; }
}

class StackLinkedList {
    private Node top;

    public void push(int x) {
        Node node = new Node(x);
        node.next = top;
        top = node;
    }

    public int pop() {
        if (top == null) throw new RuntimeException("Stack is empty");
        int val = top.data;
        top = top.next;
        return val;
    }

    public int peek() {
        if (top == null) throw new RuntimeException("Stack is empty");
        return top.data;
    }

    public boolean isEmpty() {
        return top == null;
    }
}
```

---

### 3. Using Java Collections Framework

- Java provides `Stack<T>`, `Deque<T>` (ArrayDeque recommended), and `LinkedList<T>` as stack implementations.

```java
import java.util.Stack;

Stack<Integer> stack = new Stack<>();
stack.push(10);
stack.push(20);
System.out.println(stack.pop()); // 20
System.out.println(stack.peek()); // 10
```

**Note:** `Deque<Integer> stack = new ArrayDeque<>();` is preferred over `Stack` class for thread safety and better performance.

---

## 🖼️ Visual Representation

```
Stack (top at right):

| 30 |  <- Top
| 20 |
| 10 |
 -----
 push(40):

| 40 |  <- Top
| 30 |
| 20 |
| 10 |
 -----
```

---

## 🌟 Applications & Use Cases

- Function call/recursion management (call stack)
- Undo mechanisms in editors
- Expression evaluation and syntax parsing
- Depth-First Search (DFS) in graphs/trees
- Balancing symbols (parentheses, brackets)
- Backtracking algorithms

---

## 💡 Common Stack Interview Problems

1. **Implement a Stack using Queues**
2. **Implement a Queue using Stacks**
3. **Evaluate Reverse Polish Notation (Postfix Expression)**
4. **Balanced Parentheses/Brackets**
5. **Min Stack (get minimum in O(1) time)**
6. **Sort a Stack using Another Stack**
7. **Next Greater Element (NGE)**
8. **Design a Stack with getMiddle() in O(1)**
9. **Largest Rectangle in Histogram**
10. **Stock Span Problem**

---

> **Tip:** Understanding stacks is crucial for mastering recursion, parsing algorithms, and many coding interview questions!
