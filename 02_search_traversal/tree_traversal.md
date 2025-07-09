# Tree Traversal Patterns

## 1. Tree Traversal - Level Order (BFS)

**PSEUDOCODE:**
```
1. Initialize queue with root, result = []
2. WHILE queue is not empty:
   a. level_size = queue.size()
   b. level = []
   c. FOR i from 0 to level_size-1:  # Process THIS layer: multiple nodes per layer
      - node = queue.dequeue()
      - level.append(node.val)        # Process this node
      - IF node.left: queue.enqueue(node.left)   # Add children for next layer
      - IF node.right: queue.enqueue(node.right)
   d. result.append(level)
3. Return result
```

**TIME:** O(n), **SPACE:** O(w) where w is max width  
**USE:** Level order traversal, zigzag traversal, right/left side view, minimum depth

---

## 2. Tree Traversal - Inorder (DFS)

**PSEUDOCODE:**
```
1. Initialize stack = [], current = root, result = []
2. WHILE current OR stack is not empty:
   a. WHILE current:
      - stack.push(current)
      - current = current.left        # Go deeper (left)
   b. current = stack.pop()
   c. result.append(current.val)      # Process THIS layer: one node per layer
   d. current = current.right         # Go deeper (right)
3. Return result
```

**TIME:** O(n), **SPACE:** O(h) where h is height  
**USE:** BST validation, kth smallest element, inorder successor, tree serialization 