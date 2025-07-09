# Sliding Window Patterns

## Fixed-Size Sliding Window

**PSEUDOCODE:**
```
1. IF array length < window_size: return 0
2. Calculate initial window sum (first k elements)
3. Set result = initial window sum
4. FOR i from k to n-1:
   a. Remove leftmost element: sum -= arr[i-k]
   b. Add new element: sum += arr[i]
   c. Update result (max/min as needed)
5. Return result
```

**TIME:** O(n), **SPACE:** O(1)  
**USE:** Maximum/minimum sum of k consecutive elements

**EXAMPLE:**
```
arr = [2, 1, 5, 1, 3, 2], k = 3
Initial window: [2, 1, 5] = 8
Slide: [1, 5, 1] = 7
Slide: [5, 1, 3] = 9 ← Max
Slide: [1, 3, 2] = 6
Result: 9
```

---

## Variable-Size Sliding Window

**PSEUDOCODE:**
```
1. Initialize left = 0, current_sum = 0, result = 0
2. FOR right from 0 to n-1:
   a. Add arr[right] to current_sum  # Expand window
   b. WHILE condition is met (e.g., sum >= target):
      - Update result (min length, count, etc.)
      - Remove arr[left] from current_sum  # Shrink window
      - left++
3. Return result
```

**TIME:** O(n), **SPACE:** O(1)  
**USE:** Smallest subarray with sum >= target, longest subarray with unique chars

**DETAILED STEPS:**
- **Window expansion**: Add new element to current state
- **Window contraction**: Remove elements until condition is violated
- **Result tracking**: Update answer during contraction phase
- **Two-pointer movement**: Left moves only when condition is met

**COMMON CONDITIONS:**
- **Sum >= target**: Find minimum length subarray
- **Unique characters**: Track character frequency
- **At most k distinct**: Count distinct elements

**EXAMPLE:** Smallest subarray with sum >= target
- Expand: Add elements until sum >= target
- Contract: Remove elements while sum >= target
- Track: Minimum length during contraction 

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