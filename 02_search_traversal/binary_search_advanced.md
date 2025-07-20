# Advanced Binary Search Patterns

## 1. Advanced Binary Search - Range Queries with Multiple Operations

**PSEUDOCODE:**
```
1. Binary Search Left (>= target, start_pos):
   left, right = start_pos, n
   ans = n
   
   WHILE left < right:
      mid = (left + right) // 2
      IF arr[mid] < target:
         left = mid + 1
      ELSE:
         ans = mid
         right = mid
   
   RETURN ans

2. Binary Search Right (> target, start_pos):
   left, right = start_pos, n
   ans = n
   
   WHILE left < right:
      mid = (left + right) // 2
      IF arr[mid] <= target:
         left = mid + 1
      ELSE:
         ans = mid
         right = mid
   
   RETURN ans

3. Range Query with Bucket Processing:
   a. left = binary_search_left(arr, window_start, 0)
   b. right = binary_search_right(arr, window_start + window_size - 1, 0)
   c. Extract window: arr[left:right]
   d. Process window with bucket-based logic

4. Bucket Processing with Consecutive Miss Detection:
   a. consecutive_misses = 0, p = 0
   b. FOR each bucket in window:
      - b_start = window_start + bucket_size * i
      - b_end = b_start + bucket_size - 1
      - p = binary_search_left(window_times, b_start, p)
      - IF p < len(window_times) AND window_times[p] <= b_end:
         - consecutive_misses = 0 (reset)
         - p = binary_search_right(window_times, b_end, p)
      - ELSE:
         - consecutive_misses++
         - IF consecutive_misses >= 3: return False
   c. RETURN True
```

**TIME:** O(log n) per query, **SPACE:** O(n)  
**USE:** Range queries, window-based processing, consecutive failure detection

**KEY INSIGHTS:**
- **Range Extraction**: Use binary search to find window boundaries
- **Bucket Processing**: Divide window into smaller buckets for analysis
- **Consecutive Logic**: Reset miss counter on any hit, increment on miss
- **Position Tracking**: Use start_pos to avoid reprocessing same elements

**EXAMPLE USES:**
- Heartbeat monitoring with consecutive miss detection
- Health check systems with failure thresholds
- Time series analysis with window processing 