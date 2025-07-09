# Backtracking Patterns

## 1. Multiple Choices Per Layer Backtracking

**PSEUDOCODE:**
```
res = []

backtrack(path, start):
    if path condition meet:
        add copy of path to res
    
    for i in start to n-1:  # Process THIS layer: multiple choices per layer
        add ele to path      # Try this choice
        backtrack(path, i+1) # Go deeper
        path.pop()           # Undo this choice, try next

return res
```

**TIME:** O(n!) for permutations, O(2^n) for subsets, **SPACE:** O(n)
**USE:** Subsets, combinations, permutations, all paths from root to leaf, all paths in grid

---

## 2. Grid Backtracking

**PSEUDOCODE:**
```
findNextEmpty(grid):
    for row in 0 to m - 1:
        for col in 0 to n - 1:
            if grid[row][col] is empty:
                return row, col
    return -1, -1

backtrack(grid):
    row, col = findNextEmpty(grid)
    if row == -1:
        return True
    for choice in all possible choices:  # Process THIS layer: one cell per layer
        if isValid(grid, row, col, choice):
            grid[row][col] = choice      # Try this choice
            if backtrack(grid):          # Go deeper
                return True
            set grid[row][col] empty     # Undo this choice, try next
    return False
```

**TIME:** O(9^(n²)), **SPACE:** O(n²)
**USE:** Sudoku solver, N-Queens, Word Search 