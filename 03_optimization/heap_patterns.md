# Heap/Priority Queue Patterns

## 1. Top K Elements

**PSEUDOCODE:**
```
1. Create min heap (for top k largest) or max heap (for top k smallest)
2. FOR each element in array:
   a. Add element to heap
   b. IF heap size > k:
      - Remove min/max element
3. Return heap elements
```

**TIME:** O(n log k), **SPACE:** O(k)  
**USE:** Find top k largest/smallest elements

**EXAMPLE:**
```
Input: [3,1,5,2,4], k = 3
Step 1: Create min heap
Step 2: Add 3 → [3]
        Add 1 → [1,3]
        Add 5 → [1,3,5]
        Add 2 → [1,2,3,5] → remove 1 → [2,3,5]
        Add 4 → [2,3,4,5] → remove 2 → [3,4,5]
Output: [3,4,5]
```

---

## 2. Merge K Sorted Lists

**PSEUDOCODE:**
```
1. Create min heap
2. Add first element of each list to heap with (value, list_index, element_index)
3. WHILE heap is not empty:
   a. Remove min element from heap
   b. Add to result
   c. IF next element exists in same list:
      - Add next element to heap
4. Return merged result
```

**TIME:** O(n log k), **SPACE:** O(k)  
**USE:** Merge k sorted linked lists

---

## 3. Find Median from Data Stream

**PSEUDOCODE:**
```
1. Create max_heap (left half) and min_heap (right half)
2. FOR each number:
   a. Add to max_heap
   b. Move largest from max_heap to min_heap
   c. IF min_heap size > max_heap size:
      - Move smallest from min_heap to max_heap
3. Median = max_heap.top() (odd) or (max_heap.top() + min_heap.top()) / 2 (even)
```

**TIME:** O(log n) per insertion, O(1) for median  
**SPACE:** O(n)  
**USE:** Find median of streaming data

---

## 4. Sliding Window Median

**PSEUDOCODE:**
```
1. Create two heaps (max_heap, min_heap) with removal tracking
2. FOR each window:
   a. Add new element to appropriate heap
   b. Remove old element (mark as removed)
   c. Balance heaps
   d. Calculate median
3. Return medians for all windows
```

**TIME:** O(n log k), **SPACE:** O(k)  
**USE:** Find median for each sliding window

---

## 5. K Closest Points to Origin

**PSEUDOCODE:**
```
1. Create max heap (keep k closest)
2. FOR each point:
   a. Calculate distance = sqrt(x² + y²)
   b. Add (-distance, point) to heap (negative for max heap)
   c. IF heap size > k:
      - Remove farthest point
3. Return k closest points
```

**TIME:** O(n log k), **SPACE:** O(k)  
**USE:** Find k closest points to origin

---

## 6. Last Stone Weight

**PSEUDOCODE:**
```
1. Create max heap with all stone weights
2. WHILE heap size > 1:
   a. Remove two largest stones
   b. IF stones are different:
      - Add difference back to heap
3. Return remaining stone weight or 0
```

**TIME:** O(n log n), **SPACE:** O(n)  
**USE:** Find weight of last remaining stone 