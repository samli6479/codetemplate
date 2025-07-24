# Two Pointers Patterns

## Opposite Ends (Converging)

**PSEUDOCODE:**
```
1. Initialize left = 0, right = n-1
2. WHILE left < right:
   a. Calculate current_sum = arr[left] + arr[right]
   b. IF current_sum == target: return [left, right]
   c. ELSE IF current_sum < target: left++
   d. ELSE: right--
3. Return not found
```

**TIME:** O(n), **SPACE:** O(1)  
**USE:** Two sum in sorted array, container with most water

**EXAMPLE:**
```
arr = [2, 7, 11, 15], target = 9
left=0, right=3: 2+15=17 > 9, right--
left=0, right=2: 2+11=13 > 9, right--
left=0, right=1: 2+7=9 == target, return [0,1]
```

---

## Same Direction (Tandem)

**PSEUDOCODE:**
```
1. Initialize write_index = 0
2. FOR read_index from 0 to n-1:
   a. IF condition met (e.g., arr[read_index] != 0):
      - arr[write_index] = arr[read_index]
      - write_index++
3. Return write_index (new length)
```

**TIME:** O(n), **SPACE:** O(1)  
**USE:** Remove duplicates, move zeros to end

**EXAMPLE:**
```
arr = [0, 1, 0, 3, 12]
read=0: 0, skip
read=1: 1, write to index 0, write_index=1
read=2: 0, skip  
read=3: 3, write to index 1, write_index=2
read=4: 12, write to index 2, write_index=3
Result: [1, 3, 12, _, _], length=3
```

---

## Fast/Slow Pointers

### Basic: Find Middle Node

**PSEUDOCODE:**
```
1. slow = fast = head
2. WHILE fast and fast.next:
   a. slow = slow.next
   b. fast = fast.next.next
3. Return slow
```

**TIME:** O(n), **SPACE:** O(1)  
**USE:** Find middle node of linked list

**EXAMPLE:**
```
List: 1 -> 2 -> 3 -> 4 -> 5
slow: 1, 2, 3
fast: 1, 3, 5
Result: slow = 3 (middle node)
```

### Advanced: Cycle Detection & Start

**PSEUDOCODE:**
```
1. slow = fast = head
2. WHILE fast and fast.next:
   a. slow = slow.next
   b. fast = fast.next.next
   c. IF slow == fast: break (cycle detected)
3. IF not fast or not fast.next: return null (no cycle)
4. point = head
5. WHILE point != slow:
   a. point = point.next
   b. slow = slow.next
6. Return point (cycle start)
```

**TIME:** O(n), **SPACE:** O(1)  
**USE:** Detect cycle and find cycle start

**EXAMPLE:**
```
List: 1 -> 2 -> 3 -> 4 -> 2 (cycle back to 2)
Step 1: Find meeting point
slow: 1, 2, 3, 4, 2, 3, 4, 2...
fast: 1, 3, 2, 4, 3, 2, 4, 3...
Meeting at node 2: cycle detected

Step 2: Find cycle start
point: 1, 2
slow: 2, 3
Meeting at node 2: cycle starts at node 2
``` 