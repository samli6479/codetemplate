# Merge Intervals

**PSEUDOCODE:**
```
1. Sort intervals by start time
2. merged = []
3. FOR each interval in sorted order:
   a. IF merged is empty OR start > merged[-1].end:
      - add interval to merged
   b. ELSE:
      - merged[-1].end = max(merged[-1].end, end)
4. Return merged
```

**DETAILED STEPS:**
- **Sort first**: Sort intervals by start time to ensure proper order
- **Linear scan**: Process each interval in sorted order
- **Overlap check**: Compare current interval with last merged interval
- **Merge or append**: Either merge overlapping intervals or add new one

**EXAMPLE 1: Basic Merge**
```
intervals = [[1,3], [2,6], [8,10], [15,18]]
sorted = [[1,3], [2,6], [8,10], [15,18]]
merged = [[1,6], [8,10], [15,18]]
```

**EXAMPLE 2: Multiple Overlaps**
```
intervals = [[1,4], [4,5], [2,3], [6,8]]
sorted = [[1,4], [2,3], [4,5], [6,8]]
merged = [[1,5], [6,8]]
```

**EXAMPLE 3: Complete Overlap**
```
intervals = [[1,4], [2,3], [3,4], [5,6]]
sorted = [[1,4], [2,3], [3,4], [5,6]]
merged = [[1,4], [5,6]]
```

**TIME:** O(n log n), **SPACE:** O(n)  
**USE:** Meeting rooms, calendar scheduling, overlapping intervals, time range consolidation 