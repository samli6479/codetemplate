# Array Scanning Patterns

## 1. Next/Previous Permutation

**PSEUDOCODE:**
```
1. Initialize pivot = -1

2. Find pivot (first decreasing element from right):
   FOR i from n-2 to 0:
      IF nums[i] > nums[i+1]:
         pivot = i
         break

3. IF pivot == -1:
   - Reverse entire array (already at last permutation)
   - Return

4. Find swap candidate (first element > nums[pivot] from right):
   FOR j from n-1 to 0:
      IF nums[j] > nums[pivot]:
         break

5. Swap nums[j] and nums[pivot]

6. Reverse suffix from pivot+1 to n-1

NOTE: For Previous Permutation, use opposite conditions:
- Step 2: IF nums[i] < nums[i+1] (increasing instead of decreasing)
- Step 4: IF nums[j] < nums[pivot] (smaller instead of larger)
```

**TIME:** O(n), **SPACE:** O(1)  
**USE:** Find next/previous lexicographically ordered permutation

**EXAMPLE:**
```
Next Permutation:
Input: [1, 2, 3, 4]
Step 1: pivot = -1
Step 2: Find pivot → i=2 (nums[2]=3 > nums[3]=4? No) → i=1 (nums[1]=2 > nums[2]=3? No) → i=0 (nums[0]=1 > nums[1]=2? No) → pivot = -1
Step 3: pivot == -1 → reverse all → [4, 3, 2, 1]
Output: [4, 3, 2, 1]
```

---

## 2. Single Number

**PSEUDOCODE:**
```
1. Initialize res = 0

2. FOR num in nums:
   a. res = res XOR num

3. Return res
```

**TIME:** O(n), **SPACE:** O(1)  
**USE:** Find single number in array where all others appear twice

**XOR PROPERTIES:**
- **a XOR a = 0** (number XOR itself = 0)
- **a XOR 0 = a** (number XOR 0 = number)
- **a XOR b XOR a = b** (commutative and associative)
- **a XOR b XOR b = a** (XOR is its own inverse)

**EXAMPLE:**
```
Input: [4, 1, 2, 1, 2]
Step 1: res = 0
Step 2: 0 XOR 4 = 4
        4 XOR 1 = 5
        5 XOR 2 = 7
        7 XOR 1 = 6 (1 XOR 1 = 0, so 7 XOR 1 = 6)
        6 XOR 2 = 4 (2 XOR 2 = 0, so 6 XOR 2 = 4)
Step 3: Return 4
Output: 4
```

---

## 3. Majority Element (Boyer-Moore)

**PSEUDOCODE:**
```
1. Initialize count = 0, candidate = 0

2. FOR i from 0 to n-1:
   a. IF nums[i] == candidate:
      - count++
   b. ELSE IF count == 0:
      - candidate = nums[i]
      - count = 1
   c. ELSE IF nums[i] != candidate:
      - count--

3. Return candidate
```

**TIME:** O(n), **SPACE:** O(1)  
**USE:** Find element that appears more than n/2 times

---

## 4. Majority Element II (More than n/3 times)

**PSEUDOCODE:**
```
1. Initialize count1 = count2 = 0, candidate1 = candidate2 = 0

2. FOR i from 0 to n-1:
   a. IF nums[i] == candidate1:
      - count1++
   b. ELSE IF nums[i] == candidate2:
      - count2++
   c. ELSE IF count1 == 0:
      - candidate1 = nums[i]
      - count1 = 1
   d. ELSE IF count2 == 0:
      - candidate2 = nums[i]
      - count2 = 1
   e. ELSE:
      - count1--
      - count2--

3. Verify candidates by counting their frequencies
4. Return candidates that appear more than n/3 times
```

**TIME:** O(n), **SPACE:** O(1)  
**USE:** Find elements that appear more than n/3 times

---

## 5. Majority Element K (Generalized)

**PSEUDOCODE:**
```
1. Initialize candidates[k-1] and counts[k-1] arrays
   - candidates[i] = 0, counts[i] = 0 for all i

2. FOR i from 0 to n-1:
   a. IF nums[i] matches any candidate in candidates[]:
      - increment corresponding count in counts[]
   b. ELSE IF any count in counts[] is 0:
      - replace that candidate with nums[i]
      - set count to 1
   c. ELSE:
      - decrement all counts in counts[]

3. Verify all candidates by counting frequencies
4. Return candidates that appear more than n/k times
```

**TIME:** O(n), **SPACE:** O(k)  
**USE:** Find elements that appear more than n/k times

**DATA STRUCTURES:**
- **candidates[k-1]**: Array to store k-1 potential majority elements
- **counts[k-1]**: Array to store count for each candidate
- **Example for k=3**: candidates[2], counts[2] (2 candidates, 2 counts) 