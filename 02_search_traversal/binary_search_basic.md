# Basic Binary Search Patterns

## 1. Binary Search - Standard

**PSEUDOCODE:**
```
left, right = 0, n-1

while left <= right:
    mid = (left + right) >> 1
    
    if nums[mid] == target:
        return mid
    elif nums[mid] < target:
        left = mid + 1
    elif nums[mid] > target:
        right = mid - 1

return -1
```

**TIME:** O(log n), **SPACE:** O(1)  
**USE:** Finding element in sorted array

---

## 2. Binary Search - Rightmost

**PSEUDOCODE:**
```
left, right = 0, n-1
ans = -1

while left <= right:
    mid = (left + right) >> 1
    
    if nums[mid] <= target:
        ans = mid
        left = mid + 1
    else:
        right = mid - 1

return ans
```

**TIME:** O(log n), **SPACE:** O(1)  
**USE:** Find rightmost occurrence, find insertion point

---

## 3. Binary Search - Answer Space

**PSEUDOCODE:**
```
isValid(nums, cur):
    res = 0
    for num in nums:
        res += function(num, cur)
    return res

left, right = 0, n-1
ans = -1

while left <= right:
    mid = (left + right) >> 1
    
    if isValid(nums, mid):
        ans = mid
        left = mid + 1
    else:
        right = mid - 1

return ans
```

**TIME:** O(n log M) where M is answer space, **SPACE:** O(1)  
**USE:** Capacity to ship packages, minimum time to complete tasks 