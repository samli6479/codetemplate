# Stack-Based Applications

## 1. Monotonic Stack

**PSEUDOCODE:**
```
1. Initialize stack = [], result = []
2. FOR i from 0 to n-1:
   a. WHILE stack not empty AND condition_met(stack, i):
      - Pop from stack
   b. Update result based on stack state
   c. Push current element to stack
3. Return result
```

**TIME:** O(n), **SPACE:** O(n)  
**USE:** Next greater element, largest rectangle, monotonic problems

**COMMON VARIATIONS:**
- **Next Greater**: `arr[stack[-1]] < arr[i]`
- **Next Smaller**: `arr[stack[-1]] > arr[i]`
- **Previous Greater**: Process from right to left
- **Previous Smaller**: Process from right to left

**EXAMPLE:**
```
arr = [4, 5, 2, 10, 8]
result = [5, 10, 10, -1, -1]
```

**KEY INSIGHTS:**
- Stack maintains monotonic order
- Each element pushed/popped at most once → O(n) time
- Use for "next/previous greater/smaller" problems
- Can handle both array and histogram problems

---

## 2. Stack-Based Command Pattern (Undo/Redo)

**PSEUDOCODE:**
```
1. Initialize Command Pattern:
   - buf = "" (current text buffer)
   - undo_stack = [], redo_stack = [] (operation stacks)

2. TYPE(text):
   a. undo_stack.append(("del", len(text)))
   b. redo_stack.clear()
   c. buf += text

3. DELETE(k):
   a. IF k > len(buf): k = len(buf)
   b. deleted = buf[-k:]
   c. undo_stack.append(("add", deleted))
   d. redo_stack.clear()
   e. buf = buf[:-k]

4. UNDO():
   a. IF undo_stack is empty: return
   b. op, arg = undo_stack.pop()
   c. IF op == "del":
      - chunk = buf[-arg:]
      - redo_stack.append(("add", chunk))
      - buf = buf[:-arg]
   d. ELSE: (op == "add")
      - redo_stack.append(("del", len(arg)))
      - buf += arg

5. REDO():
   a. IF redo_stack is empty: return
   b. op, arg = redo_stack.pop()
   c. IF op == "add":
      - undo_stack.append(("del", len(arg)))
      - buf += arg
   d. ELSE: (op == "del")
      - chunk = buf[-arg:]
      - undo_stack.append(("add", chunk))
      - buf = buf[:-arg]
```

**TIME:** O(1) per operation, **SPACE:** O(n) where n is total operations  
**USE:** Text editors, drawing applications, any system requiring undo/redo functionality

**EXAMPLE USES:**
- Text editor: type/delete operations with undo/redo
- Drawing app: brush strokes with undo/redo
- Command pattern: any reversible operations

---

## 3. Hybrid Stack-Snapshot Pattern (Advanced)

**PSEUDOCODE:**
```
1. Initialize Hybrid Stack-Snapshot:
   - buf = "" (current text buffer)
   - undo_stack = [], redo_stack = [] (operation stacks)
   - snapshots = {} (HashMap: id → buffer state)
   - history = [] (ordered snapshot IDs)
   - history_idx = -1 (pointer into history)
   - snapshot_counter = 0

2. TYPE(text):
   a. undo_stack.append(("del", len(text)))
   b. redo_stack.clear()
   c. buf += text

3. DELETE(k):
   a. IF k > len(buf): k = len(buf)
   b. deleted = buf[-k:]
   c. undo_stack.append(("add", deleted))
   d. redo_stack.clear()
   e. buf = buf[:-k]

4. UNDO():
   a. IF undo_stack is empty: return
   b. op, arg = undo_stack.pop()
   c. IF op == "del":
      - chunk = buf[-arg:]
      - redo_stack.append(("add", chunk))
      - buf = buf[:-arg]
   d. ELSE: (op == "add")
      - redo_stack.append(("del", len(arg)))
      - buf += arg

5. REDO():
   a. IF redo_stack is empty: return
   b. op, arg = redo_stack.pop()
   c. IF op == "add":
      - undo_stack.append(("del", len(arg)))
      - buf += arg
   d. ELSE: (op == "del")
      - chunk = buf[-arg:]
      - undo_stack.append(("add", chunk))
      - buf = buf[:-arg]

6. SNAPSHOT():
   a. snapshot_counter++
   b. sid = snapshot_counter
   c. snapshots[sid] = buf
   d. IF history_idx < len(history) - 1:
      - history = history[:history_idx + 1]
   e. history.append(sid)
   f. history_idx++
   g. return sid

7. UNDO_SNAPSHOT():
   a. IF history_idx <= 0: return
   b. history_idx--
   c. sid = history[history_idx]
   d. buf = snapshots[sid]

8. REDO_SNAPSHOT():
   a. IF history_idx >= len(history) - 1: return
   b. history_idx++
   c. sid = history[history_idx]
   d. buf = snapshots[sid]
```

**TIME:** O(1) for all operations, **SPACE:** O(n) where n is total operations + snapshots  
**USE:** Advanced text editors, version control systems, complex undo/redo

**KEY INSIGHTS:**
- **Hybrid Approach**: Combines operation-based and snapshot-based undo
- **Memory Trade-offs**: Snapshots use more memory but faster restoration
- **Complex State Management**: Multiple data structures working together
- **Real-world Applicable**: Used in professional text editors and IDEs

**EXAMPLE USES:**
- Advanced text editors with both undo/redo and snapshots
- Version control systems with branching
- Complex drawing applications with history 