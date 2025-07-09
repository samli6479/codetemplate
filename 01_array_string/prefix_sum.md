# Prefix Sum & Precomputation

## 1. Basic Prefix Sum

**PSEUDOCODE:**
```
1. Create prefix_sum array of size n+1
2. prefix_sum[0] = 0
3. FOR i from 0 to n-1:
   a. prefix_sum[i+1] = prefix_sum[i] + arr[i]
4. To get sum from i to j: prefix_sum[j+1] - prefix_sum[i]
```

**TIME:** O(n) preprocessing, O(1) query, **SPACE:** O(n)  
**USE:** Range sum queries, subarray sum problems

**EXAMPLE:**
```
arr = [1, 2, 3, 4, 5]
prefix_sum = [0, 1, 3, 6, 10, 15]
Sum from index 1 to 3: prefix_sum[4] - prefix_sum[1] = 10 - 1 = 9
```

---

## 2. Difference Array (Range Updates)

**PSEUDOCODE:**
```
1. Initialize diff array of size n+1: diff = [0] * (n+1)
2. FOR each update [start, end, inc]:
   a. diff[start] += inc
   b. diff[end + 1] -= inc
3. Reconstruct array:
   a. result[0] = diff[0]
   b. FOR i from 1 to n-1:
      - result[i] = result[i-1] + diff[i]
4. Return result
```

**TIME:** O(n + m) where m = number of updates, **SPACE:** O(n)  
**USE:** Range updates, car pooling, corporate flight bookings

**EXAMPLE:**
```
length = 5, updates = [[1, 3, 2], [2, 4, 3], [0, 2, -2]]
diff = [0, 0, 0, 0, 0, 0]

After [1, 3, 2]: diff = [0, 2, 0, 0, -2, 0]
After [2, 4, 3]: diff = [0, 2, 3, 0, -2, -3]
After [0, 2, -2]: diff = [-2, 2, 3, 0, -2, -3]

Reconstruct: result = [-2, 0, 3, 5, 3]
```

---

## 3. Prefix Sum with Hash Map

**PSEUDOCODE:**
```
1. Initialize prefix_sum = 0, count = 0, sum_count = {}
2. sum_count[0] = 1  # Empty subarray has sum 0
3. FOR each num in array:
   a. prefix_sum += num
   b. IF (prefix_sum - target) in sum_count:
      - count += sum_count[prefix_sum - target]
   c. sum_count[prefix_sum] += 1
4. Return count
```

**TIME:** O(n), **SPACE:** O(n)  
**USE:** Count subarrays with sum equal to target

**EXAMPLE:**
```
arr = [1, 1, 1], target = 2
prefix_sum: 0, 1, 2, 3
sum_count: {0:1, 1:1, 2:1, 3:1}
When prefix_sum=2: check if (2-2)=0 exists → yes, count=1
When prefix_sum=3: check if (3-2)=1 exists → yes, count=2
Result: 2 subarrays
```

---

## 4. Prefix/Suffix Scanning

**PSEUDOCODE:**
```
1. Initialize arrays:
   - prefix[n] = [0] * n
   - suffix[n] = [0] * n

2. Left→Right pass (prefix):
   a. prefix[0] = arr[0]
   b. FOR i from 1 to n-1:
      - prefix[i] = operation(prefix[i-1], arr[i])

3. Right→Left pass (suffix):
   a. suffix[n-1] = arr[n-1]
   b. FOR j from n-2 down to 0:
      - suffix[j] = operation(suffix[j+1], arr[j])

4. Use for specific problems:
   function(nums, suffix, prefix)
   - Shortest unsorted subarray: find where nums[i] != suffix[i] or prefix[i]
   - Trapping rain water: water[i] = min(prefix[i], suffix[i]) - arr[i]
   - Product except self: result[i] = prefix[i] * suffix[i]
```

**TIME:** O(n), **SPACE:** O(n)  
**USE:** Bidirectional scanning problems, running statistics

---

## Key Differences:
- **Prefix Sum**: For range sum queries
- **Difference Array**: For efficient range updates
- **Prefix/Suffix**: For running statistics (max/min/prod) and bidirectional scanning
- **Hash Map**: For counting subarrays with specific sum 