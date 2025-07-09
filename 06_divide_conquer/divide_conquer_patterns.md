# Divide & Conquer Patterns

## 1. Merge Sort

**PSEUDOCODE:**
```
1. Define merge_sort(arr, left, right):
   a. IF left >= right: return
   b. mid = (left + right) // 2
   c. merge_sort(arr, left, mid)
   d. merge_sort(arr, mid + 1, right)
   e. merge(arr, left, mid, right)

2. Define merge(arr, left, mid, right):
   a. Create temp arrays: left_arr, right_arr
   b. Copy elements to temp arrays
   c. i = j = 0, k = left
   d. WHILE i < left_size AND j < right_size:
      - IF left_arr[i] <= right_arr[j]: arr[k] = left_arr[i], i++
      - ELSE: arr[k] = right_arr[j], j++
      - k++
   e. Copy remaining elements from left_arr and right_arr
```

**TIME:** O(n log n), **SPACE:** O(n)

---

## 2. Maximum Subarray

**PSEUDOCODE:**
```
1. Define max_subarray_helper(left, right):
   a. IF left == right: return (arr[left], arr[left], arr[left], arr[left])
   b. mid = (left + right) // 2
   c. left_result = max_subarray_helper(left, mid)
   d. right_result = max_subarray_helper(mid+1, right)
   e. Combine results: total, prefix, suffix, max_subarray
2. Return max_subarray from helper(0, n-1)
```

**TIME:** O(n log n), **SPACE:** O(log n) 