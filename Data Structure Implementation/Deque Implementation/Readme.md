# 🔄 Deque (Double-Ended Queue) Notes

---

## 📖 Introduction

A **Deque** (pronounced "deck") stands for **Double-Ended Queue**. It is a generalized version of a queue where insertion and deletion of elements can be performed at both the front and the rear. Deques combine the properties of both stacks and queues.

---

## 🏷️ Key Operations

- **addFirst(x):** Insert element x at the front.
- **addLast(x):** Insert element x at the rear.
- **removeFirst():** Remove and return element from the front.
- **removeLast():** Remove and return element from the rear.
- **peekFirst():** View the element at the front.
- **peekLast():** View the element at the rear.
- **isEmpty():** Check if the deque is empty.
- **size():** Get the number of elements.

---

## 🧩 Deque Implementation Approaches

### 1. Array-Based (Circular Array)

- Uses a fixed-size array and two pointers (`front`, `rear`) that wrap around.
- Efficient for both ends, but has a size limit.

```java
class ArrayDeque {
    int[] arr;
    int front, rear, size, capacity;

    public ArrayDeque(int capacity) {
        arr = new int[capacity];
        this.capacity = capacity;
        front = 0; rear = -1; size = 0;
    }

    public void addFirst(int x) {
        if (size == capacity) throw new RuntimeException("Deque full");
        front = (front - 1 + capacity) % capacity;
        arr[front] = x;
        size++;
    }

    public void addLast(int x) {
        if (size == capacity) throw new RuntimeException("Deque full");
        rear = (rear + 1) % capacity;
        arr[rear] = x;
        size++;
    }

    public int removeFirst() {
        if (size == 0) throw new RuntimeException("Deque empty");
        int val = arr[front];
        front = (front + 1) % capacity;
        size--;
        return val;
    }

    public int removeLast() {
        if (size == 0) throw new RuntimeException("Deque empty");
        int val = arr[rear];
        rear = (rear - 1 + capacity) % capacity;
        size--;
        return val;
    }

    public int peekFirst() {
        if (size == 0) throw new RuntimeException("Deque empty");
        return arr[front];
    }

    public int peekLast() {
        if (size == 0) throw new RuntimeException("Deque empty");
        return arr[rear];
    }

    public boolean isEmpty() {
        return size == 0;
    }
}
```

---

### 2. Doubly Linked List

- Each node has pointers to both the next and previous nodes.
- No size limit unless out of memory.

```java
class Node {
    int data;
    Node prev, next;
    Node(int data) { this.data = data; }
}

class LinkedListDeque {
    Node front, rear;

    public void addFirst(int x) {
        Node node = new Node(x);
        if (front == null) {
            front = rear = node;
        } else {
            node.next = front;
            front.prev = node;
            front = node;
        }
    }

    public void addLast(int x) {
        Node node = new Node(x);
        if (rear == null) {
            front = rear = node;
        } else {
            rear.next = node;
            node.prev = rear;
            rear = node;
        }
    }

    public int removeFirst() {
        if (front == null) throw new RuntimeException("Deque empty");
        int val = front.data;
        front = front.next;
        if (front != null) front.prev = null;
        else rear = null;
        return val;
    }

    public int removeLast() {
        if (rear == null) throw new RuntimeException("Deque empty");
        int val = rear.data;
        rear = rear.prev;
        if (rear != null) rear.next = null;
        else front = null;
        return val;
    }
}
```

---

### 3. Java Collections Framework

- Java provides `Deque<T>` interface, with `ArrayDeque<T>` and `LinkedList<T>` as implementations.

```java
import java.util.Deque;
import java.util.ArrayDeque;

Deque<Integer> deque = new ArrayDeque<>();
deque.addFirst(10);
deque.addLast(20);
System.out.println(deque.removeFirst()); // 10
System.out.println(deque.removeLast());  // 20
```

---

## 🖼️ Visual Representation

```
Front [10] [15] [20] [30] Rear
addFirst(5):
Front [5] [10] [15] [20] [30] Rear
addLast(40):
Front [5] [10] [15] [20] [30] [40] Rear
removeFirst():
Front [10] [15] [20] [30] [40] Rear
removeLast():
Front [10] [15] [20] [30] Rear
```

---

## 🌟 Applications & Use Cases

- Sliding window problems (max/min in subarray)
- Palindrome checking
- Undo/Redo operations
- Browser history (forward/back)
- Level order traversal in trees (zigzag traversal)
- Scheduling algorithms

---

## 💡 Common Deque Interview Problems

1. **Sliding Window Maximum/Minimum**
2. **Palindrome Deque**
3. **Rotten Oranges (Multi-source BFS)**
4. **Implement Stack/Queue using Deque**
5. **Design Circular Deque**
6. **LRU Cache**
7. **First Non-Repeating Character in Stream**
8. **Sum of Minimums in All Subarrays**
9. **Zigzag Level Order Traversal (Binary Tree)**
10. **Maximum of All Subarrays of Size K**

---

> **Tip:** Deques are versatile and efficient for both ends. Use `ArrayDeque` in Java for fast, thread-unsafe deques, and `LinkedList` when you need a doubly linked structure!
