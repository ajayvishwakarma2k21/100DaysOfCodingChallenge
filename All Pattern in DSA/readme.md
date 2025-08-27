# DSA Pattern Atlas

![badge](https://img.shields.io/badge/DSA-Pattern%20Atlas-7aa2ff?style=for-the-badge) ![badge](https://img.shields.io/badge/Patterns-100%2B-22cc88?style=for-the-badge) ![badge](https://img.shields.io/badge/Format-Markdown-555?style=for-the-badge)

> Tip: Click the disclosure arrows to expand sections. Use Ctrl/Cmd+F to search.

## Quick Navigation
- [Arrays and Sequences](#arrays-and-sequences)
- [Strings](#strings)
- [Linked Lists](#linked-lists)
- [Stacks and Queues](#stacks-and-queues)
- [Trees](#trees)
- [Graphs](#graphs)
- [Greedy](#greedy)
- [Divide and Conquer](#divide-and-conquer)
- [Binary/Ternary Search](#binaryternary-search)
- [Dynamic Programming (Core)](#dynamic-programming-core)
- [DP Optimizations](#dp-optimizations)
- [Bit Manipulation](#bit-manipulation)
- [Math and Number Theory](#math-and-number-theory)
- [Computational Geometry](#computational-geometry)
- [Range Query and Offline Techniques](#range-query-and-offline-techniques)
- [Heaps and Priority Patterns](#heaps-and-priority-patterns)
- [Grid and Matrix](#grid-and-matrix)
- [Backtracking, Enumeration, Search](#backtracking-enumeration-search)
- [Greedy + Data Structure Hybrids](#greedy--data-structure-hybrids)
- [Advanced Data Structures](#advanced-data-structures)
- [Randomized and Probabilistic](#randomized-and-probabilistic)
- [Scheduling and Intervals](#scheduling-and-intervals)
- [Miscellaneous Patterns](#miscellaneous-patterns)

---

### Arrays and Sequences
<details>
<summary>Expand</summary>

- Sliding window (fixed-size, variable-size)
- Two pointers (opposite ends, same direction)
- Prefix sums (1D, 2D), difference arrays (1D, 2D)
- Partitioning (Lomuto/Hoare), Dutch national flag (3-way partition)
- In-place operations (swap cycles, marking, negative-index marking)
- Cyclic sort
- Kadane’s algorithm (max subarray, variants)
- Frequency counting, bucketing, pigeonhole principle
- Coordinate compression
- Sqrt decomposition (blocks)
- Meet-in-the-middle
- Subarray/subsequence enumeration patterns
- Order statistics (quickselect, median of medians)
- Majority element (Boyer–Moore)
- Randomized shuffle (Fisher–Yates)
</details>

### Strings
<details>
<summary>Expand</summary>

- Prefix function / KMP
- Z-algorithm
- Rolling hash, Rabin–Karp (single/multiple patterns, double hash)
- Aho–Corasick automaton
- Trie / compressed trie (radix)
- Suffix array (+ LCP, Kasai), suffix tree (Ukkonen), suffix automaton
- Manacher’s algorithm (palindromes)
- Palindrome tree (Eertree)
- Lyndon factorization (Duval)
- Minimal rotation
- Edit distance family (Levenshtein, Damerau, LCS)
- Anagram hashing, frequency windows
- String DP (LCS, LPS, wildcard/regex-like matching)
- Burrows–Wheeler transform basics
</details>

### Linked Lists
<details>
<summary>Expand</summary>

- Fast–slow pointers (cycle detect, cycle length, cycle start)
- Reverse (iterative/recursive), reverse in k-group
- Merge two/k lists
- Split/partition lists
- Palindrome check
- Skip list pattern (conceptual)
</details>

### Stacks and Queues
<details>
<summary>Expand</summary>

- Monotonic stack (next/prev greater/smaller, stock span)
- Monotonic queue (sliding window maximum/minimum)
- Stack-based parsing (parentheses, operators)
- Two-stack expression evaluation (infix to postfix/prefix)
- Min/Max stack, queue with two stacks
- Deque patterns (0–1 BFS, window ops)
</details>

### Trees
<details>
<summary>Expand</summary>

- DFS traversals (pre/in/post), BFS (level order, zigzag)
- Recursion patterns (root-left-right decompositions)
- Morris traversal (O(1) space)
- Binary search tree invariants (successor/predecessor)
- Lowest common ancestor (binary lifting, Euler tour + RMQ)
- Path problems (path sum, diameter, max path)
- Tree DP (subtree sums, rerooting, small-to-large)
- Heavy–Light decomposition (paths, queries)
- Centroid decomposition
- Euler tour flattening
- Persistent structures on trees (persistent segtree/Fenwick)
- Binary indexed tree on Euler tour
- Order-statistics on BST (rank/select)
</details>

### Graphs
<details>
<summary>Expand</summary>

- Graph traversals (BFS/DFS), connected components
- Topological sort (Kahn/DFS)
- Shortest paths:
  - Unweighted BFS
  - Dijkstra (binary heap, pairing heap), 0–1 BFS, Dial’s buckets
  - Bellman–Ford, SPFA (caution)
  - Floyd–Warshall (APSP), Johnson’s algorithm
- Minimum spanning tree (Kruskal + DSU, Prim)
- Disjoint set union (union by rank/size, path compression, rollback)
- Strongly connected components (Kosaraju, Tarjan)
- Bridges and articulation points (Tarjan)
- Eulerian path/circuit (Hierholzer)
- Maximum matching (bipartite: Hopcroft–Karp), general (Edmonds’ blossom)
- Network flow (Ford–Fulkerson/Edmonds–Karp, Dinic, Push–Relabel)
- Minimum cut / Max-flow min-cut
- Minimum cost flow
- DSU on tree (small-to-large merging)
- Graph coloring (bipartite check, greedy heuristics)
- Tree isomorphism hashing (AHU)
</details>

### Greedy
<details>
<summary>Expand</summary>

- Interval scheduling (earliest finish time), activity selection
- Merge intervals, insert interval
- Scheduling with deadlines/penalties, CPU task scheduling
- Huffman coding
- Fractional knapsack
- Greedy on matroids (optimality framework)
- Gas station, jump game variants
- Local-to-global exchange arguments
</details>

### Divide and Conquer
<details>
<summary>Expand</summary>

- Binary search, mergesort, quicksort
- Divide-and-conquer DP optimization
- CDQ divide and conquer (inversions in 3D, offline queries)
- Closest pair of points
- FFT/NTT via divide-and-conquer
</details>

### Binary/Ternary Search
<details>
<summary>Expand</summary>

- Classic binary search (first/last, lower/upper bound)
- Binary search on answer (monotone predicate)
- Ternary search on unimodal function
- Exponential search (unbounded)
- Bitwise binary search (on integers)
</details>

### Dynamic Programming (Core)
<details>
<summary>Expand</summary>

- 1D DP (linear transitions)
- Knapsack family (0/1, unbounded, bounded/multiple, group)
- Subset sum/partition
- LIS (O(n log n) patience sorting), counting LIS
- LCS/LPS, edit distance variants
- Digit DP
- Bitmask DP (TSP, set DP, SOS DP)
- DP on DAGs (longest path, counting paths)
- DP on trees (rerooting, paths)
- Interval DP (merge/cost problems, matrix chain)
- Palindromic DP (strings)
- Grid DP (paths with obstacles, min cost)
- Game DP (grundy, impartial games)
- Probability DP
- Counting DP (combinatorics)
- Meet-in-the-middle + DP hybrids
</details>

### DP Optimizations
<details>
<summary>Expand</summary>

- Monotonic queue optimization (convex/concave transitions)
- Divide-and-conquer optimization (quadrangle inequality)
- Knuth optimization
- Convex hull trick (CHT), Li Chao tree
- Bitset optimization
- Sqrt decomposition + DP
- Slope trick (advanced)
</details>

### Bit Manipulation
<details>
<summary>Expand</summary>

- Bit masks/subsets enumeration
- Fast exponentiation (binary power)
- Bit DP (on subsets)
- XOR tricks (unique numbers, basis/linear XOR basis)
- Brian Kernighan’s count, builtin popcount
- Gray code
- Trie on bits (max XOR pair)
</details>

### Math and Number Theory
<details>
<summary>Expand</summary>

- Sieve of Eratosthenes, segmented sieve
- GCD/LCM, extended Euclid, Bezout
- Modular arithmetic, modular inverse (Fermat/Egcd)
- Fast power mod
- Chinese remainder theorem
- Euler’s totient, Möbius function
- Primality tests (Miller–Rabin), Pollard Rho factorization
- Combinatorics: factorials/inverses, nCr, stars and bars
- Inclusion–exclusion principle
- Pigeonhole and Dirichlet principles
- Fast transforms: FFT/NTT, Walsh–Hadamard
- Polynomial ops (convolution, interpolation)
- Matrix exponentiation
</details>

### Computational Geometry
<details>
<summary>Expand</summary>

- Orientation (ccw), segment intersection, line sweep
- Convex hull (Graham/Andrew), monotone chain
- Rotating calipers (diameter, width, closest pair post-hull)
- Closest pair of points (divide-and-conquer)
- Point in polygon (ray casting, winding)
- Polygon area, shoelace
- Circle geometry basics
- KD-tree (nearest neighbors)
- Half-plane intersection (advanced)
- Delaunay/Voronoi (conceptual)
</details>

### Range Query and Offline Techniques
<details>
<summary>Expand</summary>

- Sparse table (idempotent queries: RMQ, GCD)
- Segment tree (point/range update, RMQ, RSQ), lazy propagation
- Fenwick tree / BIT (1D/2D)
- Persistent segment tree/Fenwick
- Merge sort tree
- Wavelet tree (advanced)
- Mo’s algorithm (array, queries on trees with Euler tour, Hilbert order)
- Offline queries with DSU (Kruskal offline, connectivity)
- Order statistics tree (policy-based DS)
</details>

### Heaps and Priority Patterns
<details>
<summary>Expand</summary>

- Priority queue for top-k / k-way merge
- Sliding window using heap + lazy delete
- D-ary heaps, pairing heap, Fibonacci heap (theoretical)
- Median maintenance (two heaps)
</details>

### Grid and Matrix
<details>
<summary>Expand</summary>

- Flood fill (DFS/BFS), number of islands
- Multi-source BFS
- Shortest path on grid (Dijkstra, 0–1 BFS, A*)
- 2D prefix sums, 2D difference array
- Matrix exponentiation (linear recurrences)
- Spiral/diagonal traversals
- Union-Find on grid
</details>

### Backtracking, Enumeration, Search
<details>
<summary>Expand</summary>

- Permutations/combinations/subsets generation
- N-Queens, Sudoku solver
- Hamiltonian paths/cycles (TSP brute)
- Pruning (bounds, heuristics), branch-and-bound
- Meet-in-the-middle enumeration
</details>

### Greedy + Data Structure Hybrids
<details>
<summary>Expand</summary>

- Interval partitioning (min rooms via heap)
- Activity selection with resources
- Job sequencing with deadlines (DSU/heap)
</details>

### Advanced Data Structures
<details>
<summary>Expand</summary>

- Balanced BSTs (AVL, Red–Black), Treap, Splay
- B-Tree/B+Tree (conceptual)
- Skip list (probabilistic)
- Rope, order-statistics tree
- Link–Cut tree (dynamic trees)
- Euler tour tree (dynamic connectivity)
- Binary lifting tables
- Union-Find with rollback (offline dynamic connectivity)
- Bloom filter, Cuckoo hashing (probabilistic)
</details>

### Randomized and Probabilistic
<details>
<summary>Expand</summary>

- Randomized quicksort/quickselect
- Random hashing, universal hashing
- Monte Carlo vs Las Vegas patterns
- Reservoir sampling
</details>

### Scheduling and Intervals
<details>
<summary>Expand</summary>

- Merge/insert intervals
- Meeting rooms (min rooms)
- Non-overlapping intervals max set
- Weighted interval scheduling (DP)
- Sweep line with events (start/end)
</details>

### Miscellaneous Patterns
<details>
<summary>Expand</summary>

- Top-k (heap/quickselect/streaming)
- LRU/LFU cache patterns
- Online vs offline transformations
- A* search (heuristic-guided)
- Simulation and state compression
- Rolling/online aggregates (prefix, diff, deque)
</details>

---

## How to Use
- Start with category overviews, then drill down into sub-patterns.
- Pair each pattern with a couple of canonical problems for practice.
- Keep notes of invariants, typical pitfalls, and complexity.

If you want, I can add short one-line descriptions to every bullet, or attach curated problem links under each pattern.
