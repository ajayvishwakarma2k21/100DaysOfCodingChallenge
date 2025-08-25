# 🔗 Graph Data Structure Notes

---

## 📖 Introduction

A **Graph** is a collection of nodes (vertices) connected by edges. It is a fundamental data structure for modeling relationships between entities, such as networks, social connections, maps, etc.

---

## 🏷️ Key Concepts

- **Vertex (Node):** Fundamental unit represented as a dot or circle.
- **Edge:** A connection between two vertices.
- **Directed Graph (Digraph):** Edges have direction (A → B).
- **Undirected Graph:** Edges have no direction (A—B).
- **Weighted Graph:** Edges have weights/costs.
- **Unweighted Graph:** All edges have equal weight.
- **Adjacency:** Two vertices are adjacent if connected by an edge.
- **Degree:** Number of edges incident to a vertex.

---

## 🧩 Graph Representation

### 1. Adjacency Matrix

- 2D array of size V x V where V = number of vertices.
- `matrix[i][j] = 1` if edge from i to j exists, else 0 (or weight if weighted).

```java
int V = 4;
int[][] adjMatrix = new int[V][V];
// Add edge 0-1
adjMatrix[0][1] = 1;
adjMatrix[1][0] = 1; // Undirected
```

#### Pros
- Fast edge lookup O(1)
- Simple to implement

#### Cons
- Space inefficient for sparse graphs (O(V^2) space)

---

### 2. Adjacency List

- Array/List of lists. Each vertex has a list of its neighbors.

```java
import java.util.*;

int V = 4;
List<List<Integer>> adjList = new ArrayList<>();
for (int i = 0; i < V; i++) adjList.add(new ArrayList<>());

// Add edge 0-1
adjList.get(0).add(1);
adjList.get(1).add(0); // Undirected
```

#### Pros
- Space efficient for sparse graphs (O(V + E) space)
- Easy to traverse neighbors

#### Cons
- Slower edge lookup O(V) in worst case

---

## 🛠️ Graph Implementation in Java

### Adjacency List (Generic)

```java
import java.util.*;

class Graph {
    private int V;
    private List<List<Integer>> adj;

    public Graph(int V) {
        this.V = V;
        adj = new ArrayList<>();
        for (int i = 0; i < V; i++)
            adj.add(new ArrayList<>());
    }

    // Add edge (undirected)
    public void addEdge(int u, int v) {
        adj.get(u).add(v);
        adj.get(v).add(u); // Remove for directed
    }

    // Print adjacency list
    public void printGraph() {
        for (int i = 0; i < V; i++) {
            System.out.print(i + ": ");
            for (int v : adj.get(i))
                System.out.print(v + " ");
            System.out.println();
        }
    }
}
```

---

## ⚡ Graph Traversal Algorithms

### 1. Depth-First Search (DFS)

- Recursively visits a node and all its unvisited neighbors.
- Uses stack (or recursion).

```java
void DFS(int v, boolean[] visited) {
    visited[v] = true;
    System.out.print(v + " ");
    for (int u : adj.get(v)) {
        if (!visited[u]) DFS(u, visited);
    }
}
```

### 2. Breadth-First Search (BFS)

- Visits nodes level by level.
- Uses a queue.

```java
void BFS(int s) {
    boolean[] visited = new boolean[V];
    Queue<Integer> queue = new LinkedList<>();
    visited[s] = true;
    queue.offer(s);

    while (!queue.isEmpty()) {
        int v = queue.poll();
        System.out.print(v + " ");
        for (int u : adj.get(v)) {
            if (!visited[u]) {
                visited[u] = true;
                queue.offer(u);
            }
        }
    }
}
```

---

## 🖼️ Visual Representation

```
  0 ----- 1
   \     /
     2
```
Adjacency List:
```
0: 1 2
1: 0 2
2: 0 1
```

---

## 🌟 Applications & Use Cases

- Social networks (friend suggestions)
- Web page ranking (Google PageRank)
- Routing algorithms (GPS, networks)
- Scheduling and dependency resolution (topological sort)
- Mapping and navigation
- Pathfinding (shortest path, minimum spanning tree)

---

## 💡 Common Graph Interview Problems

1. **Detect Cycle in Graph (Directed/Undirected)**
2. **Connected Components**
3. **Shortest Path (BFS/Dijkstra’s/ Bellman-Ford)**
4. **Topological Sort**
5. **Clone Graph**
6. **Minimum Spanning Tree (Prim’s/Kruskal’s)**
7. **Number of Islands**
8. **Word Ladder**
9. **Course Schedule (Prerequisite Scheduling)**
10. **Articulation Points/Bridges**

---

## ⚠️ Important Points

- Choose adjacency list for sparse graphs, adjacency matrix for dense graphs.
- For weighted graphs, store pairs (neighbor, weight) in adjacency list.
- For directed graphs, only add edge from u to v.
- Avoid revisiting nodes using a visited array or set.

---

> **Tip:** Master graph representations and traversals (DFS, BFS), then focus on problems like connectivity, shortest/longest path, and cycles!
