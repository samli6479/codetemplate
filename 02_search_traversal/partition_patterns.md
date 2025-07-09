# Partition Patterns

## 1. Dutch National Flag (Three-Way Partition)

**PSEUDOCODE:**
```
1. Initialize low = mid = 0, high = n-1
2. WHILE mid <= high:
   a. IF arr[mid] == 0: swap arr[low] and arr[mid], low++, mid++
   b. ELSE IF arr[mid] == 1: mid++
   c. ELSE: swap arr[mid] and arr[high], high--
3. Return sorted array
```

**TIME:** O(n), **SPACE:** O(1)  
**USE:** Sort colors, three-way partition

---

## 2. Quick Sort Partition

**PSEUDOCODE:**
```
1. Choose pivot (usually last element)
2. Initialize i = left - 1
3. FOR j from left to right-1:
   a. IF arr[j] <= pivot:
      - i++
      - swap arr[i] and arr[j]
4. Swap arr[i+1] and arr[right]
5. Return i+1 (pivot position)
```

**TIME:** O(n), **SPACE:** O(1)  
**USE:** Quick sort, quick select, partition array

---

## 3. Quick Select

**PSEUDOCODE:**
```
1. Define select(left, right, k):
   a. IF left == right: return arr[left]
   b. pivot_index = partition(left, right)
   c. IF k == pivot_index: return arr[k]
   d. ELSE IF k < pivot_index: return select(left, pivot_index-1, k)
   e. ELSE: return select(pivot_index+1, right, k)
2. Return select(0, n-1, k-1)
```

**TIME:** O(n) average, O(n²) worst, **SPACE:** O(1)  
**USE:** Find kth smallest element, median

---

## 4. Wiggle Sort

**PSEUDOCODE:**
```
1. FOR i from 1 to n-1:
   a. IF i is odd AND nums[i] < nums[i-1]: swap nums[i] and nums[i-1]
   b. IF i is even AND nums[i] > nums[i-1]: swap nums[i] and nums[i-1]
2. Return modified array
```

**TIME:** O(n), **SPACE:** O(1)  
**USE:** Wiggle sort, alternating array patterns 