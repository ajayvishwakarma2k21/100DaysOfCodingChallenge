# 🚦 Queue Notes

---

## 📖 Introduction

A **Queue** is a linear data structure that follows the First-In-First-Out (FIFO) principle. The element added first is the first one to be removed. Think of a queue as a line at a ticket counter—the first person in line is served first.

---

## 🏷️ Basic Operations

- **Enqueue:** Add an element to the end (rear) of the queue.
- **Dequeue:** Remove and return the element at the front.
- **Front/Peek:** View the element at the front without removing it.
- **isEmpty:** Check if the queue is empty.
- **Size:** Return the number of elements in the queue.

---

## 🧩 Queue Implementation Methods

### 1. Using Arrays

- Fixed size (static).
- Efficient if implemented as a circular queue to avoid "false overflow".

```java
class QueueArray {
    private int[] arr;
    private int front, rear, size, capacity;

    public QueueArray(int capacity) {
        this.capacity = capacity;
        arr = new int[capacity];
        front = 0; rear = -1; size = 0;
    }

    public void enqueue(int x) {
        if (size == capacity) throw new RuntimeException("Queue is full");
        rear = (rear + 1) % capacity;
        arr[rear] = x;
        size++;
    }

    public int dequeue() {
        if (size == 0) throw new RuntimeException("Queue is empty");
        int val = arr[front];
        front = (front + 1) % capacity;
        size--;
        return val;
    }

    public int peek() {
        if (size == 0) throw new RuntimeException("Queue is empty");
        return arr[front];
    }

    public boolean isEmpty() {
        return size == 0;
    }

    public int size() {
        return size;
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

class QueueLinkedList {
    private Node front, rear;

    public void enqueue(int x) {
        Node node = new Node(x);
        if (rear == null) {
            front = rear = node;
            return;
        }
        rear.next = node;
        rear = node;
    }

    public int dequeue() {
        if (front == null) throw new RuntimeException("Queue is empty");
        int val = front.data;
        front = front.next;
        if (front == null) rear = null;
        return val;
    }

    public int peek() {
        if (front == null) throw new RuntimeException("Queue is empty");
        return front.data;
    }

    public boolean isEmpty() {
        return front == null;
    }
}
```

---

### 3. Using Java Collections Framework

- Java provides `Queue<T>`, `LinkedList<T>` and `ArrayDeque<T>` (preferred) as queue implementations.

```java
import java.util.Queue;
import java.util.LinkedList;

Queue<Integer> queue = new LinkedList<>();
queue.offer(10);
queue.offer(20);
System.out.println(queue.poll()); // 10
System.out.println(queue.peek()); // 20
```

**Note:** `ArrayDeque` is faster than `LinkedList` for queue operations.

---

## 🖼️ Visual Representation

```
Front [10] [20] [30] [40] Rear
Enqueue(50):
Front [10] [20] [30] [40] [50] Rear

Dequeue():
Front [20] [30] [40] [50] Rear
```

---

## 🌟 Applications & Use Cases

- Print/job scheduling
- Order processing systems
- Breadth-First Search (BFS) in graphs/trees
- Asynchronous data transfer (IO buffers, pipelines)
- CPU and disk scheduling
- Handling of requests in web servers

---

## 💡 Common Queue Interview Problems

1. **Implement Queue using Stacks**
2. **Implement Stack using Queues**
3. **Circular Queue Implementation**
4. **LRU Cache (using Deque/Queue)**
5. **Sliding Window Maximum**
6. **Interleaving the First Half of the Queue with Second Half**
7. **Generate Binary Numbers from 1 to N using Queue**
8. **First Non-Repeating Character in a Stream**
9. **Reverse the First K Elements of a Queue**
10. **Rotting Oranges (Multi-source BFS)**

---

> **Tip:** Understanding queues is crucial for mastering scheduling problems, BFS, and real-world system designs!
