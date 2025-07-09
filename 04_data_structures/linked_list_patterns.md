# Linked List Patterns

## 1. Linked List Reversal

**PSEUDOCODE:**
```
1. Initialize prev = null, current = head
2. WHILE current:
   a. next = current.next
   b. current.next = prev
   c. prev = current
   d. current = next
3. Return prev (new head)
```

**TIME:** O(n), **SPACE:** O(1)  
**USE:** Reverse linked list, reverse k groups

**EXAMPLE:**
```
1 → 2 → 3 → 4 → null
4 → 3 → 2 → 1 → null
```

---

## 2. Fast/Slow Pointers (Cycle Detection)

**PSEUDOCODE:**
```
1. Initialize slow = fast = head
2. WHILE fast and fast.next:
   a. slow = slow.next
   b. fast = fast.next.next
   c. IF slow == fast: return true (cycle detected)
3. Return false
```

**TIME:** O(n), **SPACE:** O(1)  
**USE:** Cycle detection, find middle node

**EXAMPLE:**
```
1 → 2 → 3 → 4 → 2 (cycle)
slow: 1, 2, 3, 4, 2
fast: 1, 3, 2, 4, 3, 2 (meets at 2)
```

---

## 3. Find Middle Node

**PSEUDOCODE:**
```
1. Initialize slow = fast = head
2. WHILE fast and fast.next:
   a. slow = slow.next
   b. fast = fast.next.next
3. Return slow (middle node)
```

**TIME:** O(n), **SPACE:** O(1)  
**USE:** Find middle, palindrome check, merge sort

**EXAMPLE:**
```
1 → 2 → 3 → 4 → 5
slow: 1, 2, 3
fast: 1, 3, 5 (null)
middle: 3
```

---

## 4. Reverse K Groups

**PSEUDOCODE:**
```
1. Initialize dummy = new node, dummy.next = head, prev = dummy
2. WHILE has k nodes ahead:
   a. start = prev.next, end = start
   b. FOR i from 1 to k-1: end = end.next
   c. next_group = end.next
   d. Reverse from start to end
   e. prev.next = end, start.next = next_group
   f. prev = start
3. Return dummy.next
```

**TIME:** O(n), **SPACE:** O(1)  
**USE:** Reverse nodes in k-group

**EXAMPLE:**
```
k=2: 1→2→3→4→5 → 2→1→4→3→5
k=3: 1→2→3→4→5 → 3→2→1→4→5
```

**KEY INSIGHTS:**
- **Reversal**: Always keep track of prev, current, next
- **Fast/Slow**: Fast moves 2x speed, meets slow in cycle
- **Middle**: Fast reaches end when slow is at middle
- **K-groups**: Count nodes, reverse group, connect to next 