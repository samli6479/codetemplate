# Grid & Graph Traversal Patterns

## 1. BFS - Grid Traversal

**PSEUDOCODE:**
```
1. Initialize queue with starting position(s)
2. Initialize visited set/matrix
3. WHILE queue is not empty:
   a. current = queue.dequeue()  # Process THIS layer: one position per layer
   b. IF current is target: return steps
   c. FOR each neighbor in 4 directions:  # Process THIS layer: multiple neighbors per layer
      - IF neighbor is valid and not visited:
        * Mark as visited
        * Add to queue with steps + 1  # Add to next layer
4. Return -1 (not found)
```

**TIME:** O(m*n), **SPACE:** O(m*n)  
**USE:** Shortest path in grid, flood fill, number of islands, walls and gates

---

## 2. DFS - Grid Traversal

**PSEUDOCODE:**
```
1. Define DFS function(row, col):
   a. IF out of bounds or invalid: return
   b. Mark current cell as visited  # Process THIS layer: one cell per layer
   c. Process current cell
   d. FOR each neighbor in 4 directions:  # Process THIS layer: multiple neighbors per layer
      - DFS(neighbor_row, neighbor_col)  # Go deeper
2. Call DFS(start_row, start_col)
```

**TIME:** O(m*n), **SPACE:** O(m*n) for recursion stack  
**USE:** Connected components, island counting, path finding, flood fill

---

## 3. Multi-Source BFS

**PSEUDOCODE:**
```
1. Initialize queue with ALL starting positions
2. Initialize visited set/matrix
3. WHILE queue is not empty:
   a. current = queue.dequeue()  # Process THIS layer: one position per layer
   b. FOR each neighbor in 4 directions:  # Process THIS layer: multiple neighbors per layer
      - IF neighbor is valid and not visited:
        * Mark as visited with distance
        * Add to queue with distance + 1  # Add to next layer
4. Return distance matrix
```

**TIME:** O(m*n), **SPACE:** O(m*n)  
**USE:** Walls and gates, rotting oranges, fire spread

---

## 4. Graph Traversal - Connected Components

**PSEUDOCODE:**
```
1. Build adjacency list from edges
2. Initialize visited = set(), components = 0
3. FOR each node from 0 to n-1:  # Process THIS layer: one node per layer
   a. IF node not visited:
      - components++
      - DFS(node) to mark all connected nodes  # Go deeper
4. Return components
```

**TIME:** O(V + E), **SPACE:** O(V)  
**USE:** Number of connected components, graph validation 