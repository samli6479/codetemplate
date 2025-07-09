# Stack-Based Patterns

## 1. Stack-Based Validation (Generic)

**PSEUDOCODE:**
```
1. Initialize stack = []
2. FOR each element in sequence:
   a. IF should_push(element, stack): stack.append(element)
   b. ELIF should_pop(element, stack):
      - IF stack empty OR not matches(stack[-1], element): return false
      - stack.pop()
   c. ELSE: handle_other_cases(element, stack)
3. Return is_valid(stack)
```

- `should_push(element, stack)`: Returns True if the element should be pushed (e.g., opening bracket, normal char, etc.)
- `should_pop(element, stack)`: Returns True if the element should trigger a pop (e.g., closing bracket, backspace, etc.)
- `matches(stack[-1], element)`: Returns True if the top of the stack matches the current element (e.g., matching brackets)
- `handle_other_cases(element, stack)`: Handles any other custom logic (e.g., skip, ignore, etc.)
- `is_valid(stack)`: Returns True if the stack is in a valid state at the end (e.g., empty for valid parentheses, or join(stack) for string simulation)

**TIME:** O(n), **SPACE:** O(n)  
**USE:** Parentheses/bracket validation, backspace string, path simplification, custom stack-based string simulation

**EXAMPLE USES:**
- Valid parentheses: push on open, pop on close, match pairs
- Backspace string: push on char, pop on '#'
- Path simplification: push on dir, pop on '..'

---

## 2. Stack-Based Expression Evaluation (Generic: +, -, *, /, Parentheses)

**PSEUDOCODE:**
```
1. Initialize stack = [], num = 0, result = 0, sign = 1, operator = '+'
2. FOR each character in expression:
   a. IF char is digit: num = num * 10 + int(char)
   b. IF char is '(': 
      - Push (result, sign, operator) to stack
      - Reset result = 0, sign = 1, operator = '+', num = 0
   c. IF char is operator OR char is ')' OR at end:
      - IF operator == '+': result += sign * num
      - IF operator == '-': result += sign * -num
      - IF operator == '*': result = result * num
      - IF operator == '/': result = int(result / num)
      - IF char in '+-*/': operator = char, num = 0
      - IF char == ')':
          - Pop (prev_result, prev_sign, prev_operator) from stack
          - result = prev_result + prev_sign * result
          - operator = prev_operator
          - num = 0
3. Return result
```

**TIME:** O(n), **SPACE:** O(n)  
**USE:** Calculator with +, -, *, /, parentheses, nested expressions

**EXAMPLE:**
```
"(2+3*(2-1))/2" → 2.5
"3+(2*2)-1" → 6
```

---

## 3. Monotonic Stack

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