# Greedy Algorithm Patterns

## 1. Interval Scheduling

**PSEUDOCODE:**
```
1. Sort intervals by end time
2. Initialize count = 0, end = -infinity
3. FOR each interval in sorted order:
   a. IF interval.start >= end:
      - count++
      - end = interval.end
4. Return count
```

**TIME:** O(n log n), **SPACE:** O(1)  
**USE:** Meeting rooms, activity selection

**EXAMPLE:**
```
Input: [[1,2], [3,4], [0,6], [5,7], [3,8], [5,9]]
Step 1: Sort by end time → [[1,2], [3,4], [0,6], [5,7], [3,8], [5,9]]
Step 2: count = 0, end = -infinity
Step 3: [1,2] → start=1 >= -infinity → count=1, end=2
        [3,4] → start=3 >= 2 → count=2, end=4
        [0,6] → start=0 < 4 → skip
        [5,7] → start=5 >= 4 → count=3, end=7
        [3,8] → start=3 < 7 → skip
        [5,9] → start=5 < 7 → skip
Output: 3
```

---

## 2. Maximum Swap

**PSEUDOCODE:**
```
1. Convert number to digits array
2. Initialize max_digit = 0, max_pos = 0, swap_pos = -1
3. Scan right to left:
   FOR i from n-1 to 0:
      a. IF digits[i] > max_digit:
         - max_digit = digits[i]
         - max_pos = i
      b. ELSE IF digits[i] < max_digit:
         - swap_pos = i
4. IF swap_pos != -1:
   - swap digits[swap_pos] and digits[max_pos]
   - return converted number
5. Return original number (no swap needed)
```

**TIME:** O(n), **SPACE:** O(n)  
**USE:** Find maximum number after at most one swap

**EXAMPLE:**
```
Input: 2736
Step 1: digits = [2,7,3,6]
Step 2: max_digit = 0, max_pos = 0, swap_pos = -1
Step 3: i=3: 6 > 0 → max_digit=6, max_pos=3
        i=2: 3 < 6 → swap_pos=2
        i=1: 7 > 6 → max_digit=7, max_pos=1
        i=0: 2 < 7 → swap_pos=0
Step 4: swap_pos=0, max_pos=1 → swap digits[0] and digits[1]
Output: 7236
```

---

## 3. Jump Game

**PSEUDOCODE:**
```
1. Initialize max_reach = 0
2. FOR i from 0 to n-1:
   a. IF i > max_reach:
      - return False
   b. max_reach = max(max_reach, i + nums[i])
   c. IF max_reach >= n-1:
      - return True
3. Return True
```

**TIME:** O(n), **SPACE:** O(1)  
**USE:** Check if can reach last index

---

## 4. Jump Game II

**PSEUDOCODE:**
```
1. Initialize jumps = 0, current_end = 0, farthest = 0
2. FOR i from 0 to n-2:
   a. farthest = max(farthest, i + nums[i])
   b. IF i == current_end:
      - jumps++
      - current_end = farthest
      c. IF current_end >= n-1:
         - break
3. Return jumps
```

**TIME:** O(n), **SPACE:** O(1)  
**USE:** Find minimum jumps to reach last index

---

## 5. Gas Station

**PSEUDOCODE:**
```
1. IF sum(gas) < sum(cost):
   - return -1
2. Initialize total = 0, start = 0
3. FOR i from 0 to n-1:
   a. total += gas[i] - cost[i]
   b. IF total < 0:
      - total = 0
      - start = i + 1
4. Return start
```

**TIME:** O(n), **SPACE:** O(1)  
**USE:** Find starting gas station to complete circuit

---

## 6. Task Scheduler

**PSEUDOCODE:**
```
1. Count frequency of each task
2. Find max_freq = maximum frequency
3. Find max_freq_count = count of tasks with max_freq
4. min_time = (max_freq - 1) * (n + 1) + max_freq_count
5. Return max(min_time, len(tasks))
```

**TIME:** O(n), **SPACE:** O(1)  
**USE:** Find minimum time to complete all tasks with cooldown 