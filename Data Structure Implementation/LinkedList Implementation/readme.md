# 🔗 Linked List in Java

---

## 📖 Introduction to Linked List

A **Linked List** is a linear data structure where elements are stored in nodes, and each node points to the next node in the sequence. Unlike arrays, linked lists do not require contiguous memory locations, making insertion and deletion operations more efficient (especially in the middle of the list).

---

## 🧩 Types of Linked Lists

### 1. Singly Linked List

```
  +-----+------+     +-----+------+     +-----+------+
  | 10  |  o-------> | 20  |  o-------> | 30  | null |
  +-----+------+     +-----+------+     +-----+------+
   head
```

### 2. Doubly Linked List

```
  null<-+-----+-----+     +-----+-----+     +-----+-----+->null
        |  1  |  o |<---> |  2  |  o |<---> |  3  |  o |
        +-----+-----+     +-----+-----+     +-----+-----+
         head
```

### 3. Circular Linked List

```
  +-----+------+
  |  5  |  o---\
  +-----+------+   \
          ^        \
          |         \
  +-----+------+     |
  | 10  |  o---/     |
  +-----+------+     |
          ^          |
          |          |
  +-----+------+     |
  | 15  |  o---/-----/
  +-----+------+
```
_All nodes are connected in a circle; the last node points back to the head._

---

## 🌟 Importance & Use Cases

- **Dynamic Memory Allocation:** No need to pre-define the size.
- **Efficient Insert/Delete:** Especially in the middle of the list, unlike arrays.
- **Implementation of Other Data Structures:** Used in stacks, queues, graphs, etc.
- **Use Cases:**
  - Undo functionality in editors
  - Browser history management
  - Implementation of adjacency lists in graphs

---

## 1️⃣ Singly Linked List

### Implementation

```java
class Node {
    int data;
    Node next;
    Node(int data) {
        this.data = data;
        this.next = null;
    }
}

class SinglyLinkedList {
    Node head;

    public void add(int data) {
        Node newNode = new Node(data);
        if (head == null) {
            head = newNode;
            return;
        }
        Node curr = head;
        while (curr.next != null) {
            curr = curr.next;
        }
        curr.next = newNode;
    }

    public boolean remove(int data) {
        if (head == null) return false;
        if (head.data == data) {
            head = head.next;
            return true;
        }
        Node curr = head;
        while (curr.next != null && curr.next.data != data) {
            curr = curr.next;
        }
        if (curr.next == null) return false;
        curr.next = curr.next.next;
        return true;
    }

    public void printList() {
        Node curr = head;
        while (curr != null) {
            System.out.print(curr.data + " -> ");
            curr = curr.next;
        }
        System.out.println("null");
    }
}
```

### Example Usage

```java
public class Main {
    public static void main(String[] args) {
        SinglyLinkedList list = new SinglyLinkedList();
        list.add(10);
        list.add(20);
        list.add(30);
        list.printList(); // 10 -> 20 -> 30 -> null
        list.remove(20);
        list.printList(); // 10 -> 30 -> null
    }
}
```

---

## 2️⃣ Doubly Linked List

### Implementation

```java
class DNode {
    int data;
    DNode prev, next;
    DNode(int data) {
        this.data = data;
        this.prev = null;
        this.next = null;
    }
}

class DoublyLinkedList {
    DNode head;

    public void add(int data) {
        DNode newNode = new DNode(data);
        if (head == null) {
            head = newNode;
            return;
        }
        DNode curr = head;
        while (curr.next != null) {
            curr = curr.next;
        }
        curr.next = newNode;
        newNode.prev = curr;
    }

    public boolean remove(int data) {
        if (head == null) return false;
        if (head.data == data) {
            head = head.next;
            if (head != null) head.prev = null;
            return true;
        }
        DNode curr = head;
        while (curr != null && curr.data != data) {
            curr = curr.next;
        }
        if (curr == null) return false;
        if (curr.prev != null) curr.prev.next = curr.next;
        if (curr.next != null) curr.next.prev = curr.prev;
        return true;
    }

    public void printForward() {
        DNode curr = head;
        while (curr != null) {
            System.out.print(curr.data + " <-> ");
            curr = curr.next;
        }
        System.out.println("null");
    }

    public void printBackward() {
        DNode curr = head;
        if (curr == null) return;
        while (curr.next != null) {
            curr = curr.next;
        }
        while (curr != null) {
            System.out.print(curr.data + " <-> ");
            curr = curr.prev;
        }
        System.out.println("null");
    }
}
```

### Example Usage

```java
public class Main {
    public static void main(String[] args) {
        DoublyLinkedList dlist = new DoublyLinkedList();
        dlist.add(1);
        dlist.add(2);
        dlist.add(3);
        dlist.printForward();   // 1 <-> 2 <-> 3 <-> null
        dlist.printBackward();  // 3 <-> 2 <-> 1 <-> null
        dlist.remove(2);
        dlist.printForward();   // 1 <-> 3 <-> null
    }
}
```

---

## 3️⃣ Circular Linked List

### Implementation

```java
class CNode {
    int data;
    CNode next;
    CNode(int data) {
        this.data = data;
        this.next = null;
    }
}

class CircularLinkedList {
    CNode last;

    public void add(int data) {
        CNode newNode = new CNode(data);
        if (last == null) {
            last = newNode;
            last.next = last;
            return;
        }
        newNode.next = last.next;
        last.next = newNode;
        last = newNode;
    }

    public boolean remove(int data) {
        if (last == null) return false;
        CNode curr = last.next, prev = last;
        do {
            if (curr.data == data) {
                if (curr == last) {
                    if (last.next == last) last = null;
                    else {
                        prev.next = curr.next;
                        last = prev;
                    }
                } else {
                    prev.next = curr.next;
                }
                return true;
            }
            prev = curr;
            curr = curr.next;
        } while (curr != last.next);
        return false;
    }

    public void printList() {
        if (last == null) {
            System.out.println("List is empty");
            return;
        }
        CNode curr = last.next;
        do {
            System.out.print(curr.data + " -> ");
            curr = curr.next;
        } while (curr != last.next);
        System.out.println("(back to head)");
    }
}
```

### Example Usage

```java
public class Main {
    public static void main(String[] args) {
        CircularLinkedList clist = new CircularLinkedList();
        clist.add(5);
        clist.add(10);
        clist.add(15);
        clist.printList(); // 5 -> 10 -> 15 -> (back to head)
        clist.remove(10);
        clist.printList(); // 5 -> 15 -> (back to head)
    }
}
```

---

## 🎯 Summary Table

| List Type          | Traversal     | Memory per Node | Insert/Delete Efficiency | Use Cases         |
|--------------------|--------------|-----------------|-------------------------|-------------------|
| Singly Linked List | Forward only | 1 pointer       | O(1) at head            | Basic structures  |
| Doubly Linked List | Both ways    | 2 pointers      | O(1) anywhere (with ref)| LRU cache, undo   |
| Circular List      | Circular     | 1/2 pointers    | Efficient round-robin    | Scheduling, games |

---

## 💡 Top 10 Important Linked List Problems (Asked in Interviews & Coding Rounds)

1. **Reverse a Linked List**  
   _Reverse the nodes of a singly linked list._

2. **Detect a Cycle in a Linked List**  
   _Check if a linked list contains a loop (cycle detection, Floyd’s algorithm)._

3. **Find the Middle of a Linked List**  
   _Find the middle node of the linked list (slow and fast pointer method)._

4. **Merge Two Sorted Linked Lists**  
   _Merge two sorted linked lists into a single sorted list._

5. **Remove N-th Node from End of List**  
   _Delete the N-th node from the end of a singly linked list._

6. **Intersection Point of Two Linked Lists**  
   _Find the node at which two singly linked lists intersect._

7. **Palindrome Linked List**  
   _Check if the linked list is a palindrome._

8. **Remove Duplicates from a Sorted Linked List**  
   _Remove duplicate nodes from a sorted linked list._

9. **Add Two Numbers Represented by Linked Lists**  
   _Each node contains a single digit; add two numbers and return as a linked list._

10. **Flatten a Multilevel Linked List**  
    _Given a linked list where nodes can have a child pointer to another list, flatten it into a single list._

---

> **Practice these problems on platforms like LeetCode, GeeksforGeeks, or HackerRank to master Linked Lists!**
