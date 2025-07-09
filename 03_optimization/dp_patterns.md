# Dynamic Programming Patterns

## 1. 1D Dynamic Programming (Bottom-Up)

**PSEUDOCODE:**
```
dp = [0] * (n+1)

base case:
    dp[0] = valueOne
    dp[1] = valueTwo

for i in 2 to n:
    dp[i] = condition(dp[i-1], dp[i-2], ...)

return dp[n]
```

**TIME:** O(n), **SPACE:** O(n)  
**USE:** Climbing stairs, house robber, fibonacci, coin change (unbounded)

**OPTIMIZATION:** Can reduce space to O(1) by keeping only last 2 values

---

## 2. 2D Grid Dynamic Programming (Bottom-Up)

**PSEUDOCODE:**
```
create dp[m][n]

dp[0][0] = base

for i in 1 to m-1:
    dp[i][0] = rowVal

for j in 1 to n-1:
    dp[0][j] = colVal

for i in 1 to m-1:
    for j in 1 to n-1:
        dp[i][j] = condition(curVal, dp[i-1][j], dp[i][j-1], dp[i-1][j-1])

return dp[m-1][n-1]
```

**TIME:** O(m*n), **SPACE:** O(m*n)  
**USE:** Minimum path sum, unique paths, LCS, edit distance, string matching

**OPTIMIZATION:** Can reduce space to O(n) by using rolling array

---

## 3. DFS with Memoization (Top-Down DP)

**PSEUDOCODE:**
```
1. Define dfs function with memoization:
   a. IF state in memo: return memo[state]  # Already computed
   b. IF base case: return base_value       # Smallest subproblem
   c. Initialize result = infinity (for min) or -infinity (for max)
   d. FOR each possible choice/transition:
      - new_state = apply_choice(current_state, choice)
      - sub_result = dfs(new_state)
      - result = min/max(result, sub_result + cost)
   e. memo[state] = result  # Store for future use
   f. return result
2. Initialize memo = {}
3. Return dfs(initial_state)
```

**DETAILED STEPS:**
- **State representation**: What defines your current position? (index, remaining_sum, etc.)
- **Base cases**: What are the smallest subproblems? (index >= n, sum == 0, etc.)
- **Choices**: What decisions can you make at each step? (take/don't take, move left/right, etc.)
- **Memoization**: Use tuple/dict to store computed results

**TIME:** O(states), **SPACE:** O(states)  
**USE:** Coin change, word break, palindrome partitioning

---

## 4. Bitmasking (State Compression DP)

**PSEUDOCODE:**
```
1. FOR mask from 0 to 2^n - 1:  # Generate all possible subsets
   a. subset = []
   b. FOR i from 0 to n-1:      # Check each bit position
      - IF mask & (1 << i):     # If bit i is set (1)
        * subset.append(arr[i]) # Include element i
   c. Process subset (count, sum, validate, etc.)
2. Return result
```

**DETAILED STEPS:**
- **Bit representation**: Each bit represents inclusion/exclusion of an element
- **Mask generation**: 0 = empty set, 1 = first element, 2 = second element, 3 = first+second, etc.
- **Bit checking**: `mask & (1 << i)` checks if bit i is set
- **Common operations**: 
  * Count set bits: `bin(mask).count('1')`
  * Add element: `mask | (1 << i)`
  * Remove element: `mask & ~(1 << i)`

**TIME:** O(2^n), **SPACE:** O(2^n)  
**USE:** Subset generation, state compression DP, traveling salesman 