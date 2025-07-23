# Sliding Window Patterns

## Fixed-Size Sliding Window

**PSEUDOCODE:**
```
1. sums = 0
2. FOR i from 0 to k-1:
   a. sums += nums[i]
3. res = sums
4. FOR i from k to n-1:
   a. sums += nums[i]
   b. sums -= nums[i-k]
   c. res = max(res, sums)
5. Return res
```

**TIME:** O(n), **SPACE:** O(1)  
**USE:** Maximum/minimum sum of k consecutive elements

**EXAMPLE:**
```
nums = [2, 1, 5, 1, 3, 2], k = 3
Phase 1: Build initial window
sums = 2 + 1 + 5 = 8
res = 8

Phase 2: Slide window
i=3: sums = 8 + 1 - 2 = 7, res = max(8,7) = 8
i=4: sums = 7 + 3 - 1 = 9, res = max(8,9) = 9
i=5: sums = 9 + 2 - 5 = 6, res = max(9,6) = 9
Result: 9
```

---

## Variable-Size Sliding Window

### Pattern 1: Update When Condition is MET

**PSEUDOCODE:**
```
1. Initialize left = 0, result = 0, window_state = {}
2. FOR right from 0 to n-1:
   a. Add arr[right] to window_state  # Expand window
   b. WHILE condition is MET (e.g., len(window) < k):
      - Update result (max length, count, etc.)
      - Remove arr[left] from window_state  # Shrink window
      - left++
3. Return result
```

**TIME:** O(n), **SPACE:** O(1)  
**USE:** Longest subarray with unique chars, exactly k distinct elements

**EXAMPLE:** Longest substring with at most 2 distinct characters
```
nums = [1,2,1,2,3], k = 2
window = {1,2} → res = 2 (while condition MET)
window = {1,2,1} → res = 3 (while condition MET)
window = {1,2,1,2} → res = 4 (while condition MET)
window = {1,2,1,2,3} → shrink until {2,3} → res = 4
```

### Pattern 2: Update When Condition is BROKEN

**PSEUDOCODE:**
```
1. Initialize left = 0, result = 0, window_state = {}
2. FOR right from 0 to n-1:
   a. Add arr[right] to window_state  # Expand window
   b. WHILE condition is BROKEN (e.g., len(window) > k):
      - Remove arr[left] from window_state  # Shrink window
      - left++
   c. Update result (max length, count, etc.)  # After while loop
3. Return result
```

**TIME:** O(n), **SPACE:** O(1)  
**USE:** Longest subarray with at most k distinct, at most target sum

**EXAMPLE:** Longest subarray with at most 2 distinct elements
```
nums = [1,2,1,2,3], k = 2
window = {1,2} → res = 2 (condition good)
window = {1,2,1} → res = 3 (condition good)
window = {1,2,1,2} → res = 4 (condition good)
window = {1,2,1,2,3} → shrink to {2,3} → res = 4 (condition good)
```

**WHEN TO USE EACH PATTERN:**
- **Pattern 1 (Condition MET)**: "At least k", "Exactly k", simple constraints
- **Pattern 2 (Condition BROKEN)**: "At most k", complex constraints, when shrinking until valid

---

## **PROBLEM TYPES & DATA STRUCTURES**

### **Distinct Elements Problems**
**Problem:** "At most k distinct elements", "Longest substring with unique chars"
**Data Structure:** `set()` + `count` variable
**Space:** O(k) where k = distinct elements
**Example:**
```python
seen = set()
count = 0
if nums[right] not in seen:
    count += 1
    seen.add(nums[right])
```

### **Frequency Problems**  
**Problem:** "At most k occurrences", "Character frequency"
**Data Structure:** `dict()` or `Counter()`
**Space:** O(k) where k = distinct elements
**Example:**
```python
numFreq = {}
numFreq[nums[right]] = numFreq.get(nums[right], 0) + 1
```

### **Sum Problems**
**Problem:** "Subarray with sum >= target", "Minimum size subarray"
**Data Structure:** Just `sum` variable
**Space:** O(1)
**Example:**
```python
current_sum = 0
current_sum += nums[right]
```

### **Binary Problems**
**Problem:** "At most k zeros", "Binary subarray"
**Data Structure:** Just `count` variable
**Space:** O(1)
**Example:**
```python
zero_count = 0
if nums[right] == 0:
    zero_count += 1
```

### **Bounded Integer Problems**
**Problem:** "Elements 0-1000", "Small range integers"
**Data Structure:** `boolean array`
**Space:** O(1) if bounded
**Example:**
```python
seen = [False] * 1001
if not seen[nums[right]]:
    seen[nums[right]] = True
``` 

---

## Common Variations
- Longest substring without repeating characters
- Longest/shortest subarray with sum at least/at most K
- Count distinct elements in each window
- Maximum/minimum in each window (can use deque for O(n))

---

## Tips
- Use a hash map or counter for character/element frequencies
- For fixed-size, only one pointer moves; for variable-size, both pointers move
- Always check window validity before shrinking
- Practice with both array and string problems 