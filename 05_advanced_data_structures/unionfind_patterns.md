# Union-Find (Disjoint Set Union) Patterns

## 1. Basic Union-Find Operations

**PSEUDOCODE:**
```
1. Initialize parent array: parent[i] = i
2. Define find(x):
   a. IF parent[x] != x: parent[x] = find(parent[x])
   b. Return parent[x]
3. Define union(x, y):
   a. root_x = find(x), root_y = find(y)
   b. IF root_x != root_y: parent[root_x] = root_y
```

**TIME:** O(n α(n)), **SPACE:** O(n)  
**USE:** Connected components, cycle detection

**EXAMPLE:**
```
Input: n = 5, edges = [[0,1], [1,2], [3,4]]
Step 1: parent = [0,1,2,3,4]
Step 2: union(0,1) → parent = [1,1,2,3,4]
Step 3: union(1,2) → parent = [1,2,2,3,4]
Step 4: union(3,4) → parent = [1,2,2,4,4]
Result: 2 connected components
```

---

## 2. Number of Connected Components

**PSEUDOCODE:**
```
1. Initialize parent array and count = n
2. FOR each edge [u, v]:
   a. root_u = find(u), root_v = find(v)
   b. IF root_u != root_v:
      - union(root_u, root_v)
      - count--
3. Return count
```

**TIME:** O(n α(n)), **SPACE:** O(n)  
**USE:** Count number of connected components in graph

---

## 3. Cycle Detection

**PSEUDOCODE:**
```
1. Initialize parent array
2. FOR each edge [u, v]:
   a. root_u = find(u), root_v = find(v)
   b. IF root_u == root_v:
      - return True (cycle found)
   c. ELSE:
      - union(root_u, root_v)
3. Return False (no cycle)
```

**TIME:** O(n α(n)), **SPACE:** O(n)  
**USE:** Detect cycles in undirected graph

---

## 4. Redundant Connection

**PSEUDOCODE:**
```
1. Initialize parent array
2. FOR each edge [u, v]:
   a. root_u = find(u), root_v = find(v)
   b. IF root_u == root_v:
      - return [u, v] (redundant edge)
   c. ELSE:
      - union(root_u, root_v)
3. Return [] (no redundant edge)
```

**TIME:** O(n α(n)), **SPACE:** O(n)  
**USE:** Find redundant connection in graph

---

## 5. Graph Valid Tree

**PSEUDOCODE:**
```
1. Initialize parent array and count = n
2. FOR each edge [u, v]:
   a. root_u = find(u), root_v = find(v)
   b. IF root_u == root_v:
      - return False (cycle found)
   c. ELSE:
      - union(root_u, root_v)
      - count--
3. Return count == 1 (single connected component)
```

**TIME:** O(n α(n)), **SPACE:** O(n)  
**USE:** Check if graph is valid tree

---

## 6. Minimum Cost to Connect All Points

**PSEUDOCODE:**
```
1. Calculate all edge distances
2. Sort edges by distance (Kruskal's algorithm)
3. Initialize parent array and total_cost = 0
4. FOR each edge [u, v, cost] in sorted order:
   a. root_u = find(u), root_v = find(v)
   b. IF root_u != root_v:
      - union(root_u, root_v)
      - total_cost += cost
5. Return total_cost
```

**TIME:** O(n² log n), **SPACE:** O(n²)  
**USE:** Find minimum cost to connect all points 