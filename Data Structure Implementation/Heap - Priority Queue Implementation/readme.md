# 🏔️ Heap & Priority Queue Notes

---

## 📖 Introduction

A **Heap** is a special complete binary tree-based data structure that satisfies the heap property:
- **Max Heap:** Parent node’s key is always greater than or equal to its children.
- **Min Heap:** Parent node’s key is always less than or equal to its children.

A **Priority Queue** is an abstract data type where each element has a priority, and elements are served based on their priority (not just their order in the queue). Heaps are commonly used to implement priority queues.

---

## 🏷️ Key Properties

- **Complete Binary Tree:** All levels are completely filled except possibly the last, which is filled from left to right.
- **Heap Property:** For every node, the value is either greater than or less than its children (depending on max/min heap).
- **Access:** The root node always contains the highest (max-heap) or lowest (min-heap) priority element.
- **Insertion/Deletion:** Both operations take O(log n) time.

---

## 🧩 Types of Heaps

- **Binary Heap:** Each node has up to two children (common for priority queues).
- **d-ary Heap:** Each node has up to d children.
- **Fibonacci Heap:** More advanced, supports faster amortized time for decrease-key and merge operations (rare in interviews).
- **Leftist Heap, Binomial Heap:** Other specialized heaps.

---

## 🖼️ Visual Representation

### Min Heap Example
```
        2
      /   \
     3     4
    / \   /
   5   7 6
```
- The smallest element (2) is always at the root.

### Max Heap Example
```
        9
      /   \
     7     6
    / \   /
   5   3 2
```
- The largest element (9) is always at the root.

---

## ⚡ Heap Operations

### 1. Insertion
- Add the element at the end (bottom-rightmost position).
- Heapify up: Bubble up to restore heap property.

### 2. Deletion (Remove Root)
- Remove the root node (highest/lowest priority).
- Replace root with the last element.
- Heapify down: Bubble down to restore heap property.

---

## 🛠️ Java Implementation

### Using Array (Manual Implementation)

```java
class MinHeap {
    int[] heap;
    int size;

    MinHeap(int capacity) {
        heap = new int[capacity];
        size = 0;
    }

    void insert(int val) {
        if (size == heap.length) throw new RuntimeException("Heap full");
        heap[size] = val;
        int i = size++;
        while (i > 0 && heap[i] < heap[(i-1)/2]) {
            int temp = heap[i];
            heap[i] = heap[(i-1)/2];
            heap[(i-1)/2] = temp;
            i = (i-1)/2;
        }
    }

    int removeMin() {
        if (size == 0) throw new RuntimeException("Heap empty");
        int min = heap[0];
        heap[0] = heap[--size];
        heapify(0);
        return min;
    }

    void heapify(int i) {
        int left = 2*i+1, right = 2*i+2, smallest = i;
        if (left < size && heap[left] < heap[smallest]) smallest = left;
        if (right < size && heap[right] < heap[smallest]) smallest = right;
        if (smallest != i) {
            int temp = heap[i];
            heap[i] = heap[smallest];
            heap[smallest] = temp;
            heapify(smallest);
        }
    }
}
```

### Using Java Collections Framework

```java
import java.util.PriorityQueue;

PriorityQueue<Integer> minHeap = new PriorityQueue<>(); // Min-heap by default
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder()); // Max-heap

minHeap.offer(10);
minHeap.offer(5);
System.out.println(minHeap.poll()); // 5 (smallest)
```

---

## 🌟 Applications & Use Cases

- Implementing **priority queues**
- **Heap sort** algorithm
- **Dijkstra’s** and **Prim’s** algorithms for shortest path/minimum spanning tree
- **Scheduling** systems (CPU, bandwidth, etc.)
- **Order statistics** (finding kth largest/smallest element)
- **Merging k sorted lists/arrays**

---

## 💡 Common Heap/Priority Queue Interview Problems

1. **Kth Largest/Smallest Element in Array**
2. **Merge K Sorted Lists/Arrays**
3. **Find Median from Data Stream**
4. **Top K Frequent Elements**
5. **Sliding Window Maximum/Minimum**
6. **Connect N Ropes with Minimum Cost**
7. **Running Median**
8. **Rearrange String with No Adjacent Duplicates**
9. **Sort Characters by Frequency**
10. **Find the Closest K Points to the Origin**

---

> **Tip:** Practice using both custom and built-in heap implementations and understand when to use min-heap vs. max-heap for problem-solving!
