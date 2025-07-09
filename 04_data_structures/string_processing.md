# String Processing Patterns

## 1. Linear String Processing

**PSEUDOCODE:**
```
1. Initialize result = [], count = 1, current = s[0]
2. FOR i from 1 to n-1:
   a. IF s[i] == current: count++
   b. ELSE: 
      - process_current(current, count)
      - current = s[i], count = 1
3. process_current(current, count)
4. Return result
```

**TIME:** O(n), **SPACE:** O(n)  
**USE:** String encoding, compression, run-length encoding

**EXAMPLE:**
```
"aaabbc" → "3a2b1c"
"abc" → "1a1b1c"
```

---



## 2. Recursive Pattern Matching

**PSEUDOCODE:**
```
1. Define function match(s, p, i, j):
   a. IF j == len(p): return i == len(s)
   b. IF j+1 < len(p) AND p[j+1] == '*':
      - IF match(s, p, i, j+2): return true  # Skip pattern
      - IF i < len(s) AND (p[j] == '.' OR p[j] == s[i]):
         - IF match(s, p, i+1, j): return true  # Match one more
      - return false
   c. IF i < len(s) AND (p[j] == '.' OR p[j] == s[i]):
      - return match(s, p, i+1, j+1)
   d. return false
2. Return match(s, p, 0, 0)
```

**TIME:** O(mn), **SPACE:** O(mn)  
**USE:** Regular expression matching, pattern matching with wildcards

**EXAMPLE:**
```
s = "aa", p = "a*" → true
s = "ab", p = ".*" → true
s = "mississippi", p = "mis*is*p*." → false
```

---

## 3. Recursive Parsing with Position Tracking

**PSEUDOCODE:**
```
1. Define function parse(s, i):
   a. Initialize result = "", count = 0
   b. WHILE i < len(s) AND s[i] != end_marker:
      - IF s[i] is digit: count = count * 10 + digit
      - IF s[i] == start_marker:
         - i++, sub_result = parse(s, i)
         - result += sub_result * count
      - IF s[i] == end_marker: return result, i+1
      - IF s[i] is valid_char: result += s[i]
      - i++
   c. Return result
2. Return parse(s, 0)
```

**TIME:** O(n), **SPACE:** O(n)  
**USE:** Nested string decoding, chemical formula parsing, recursive parsing

**EXAMPLE:**
```
Chemical: "Mg(OH)2" → {"Mg": 1, "O": 2, "H": 2}
Decoding: "3[a]2[bc]" → "aaabcbc"
```

**KEY INSIGHTS:**
- Use recursion for nested structures
- Track position with index parameter
- Handle base cases and recursive cases
- Return both result and updated position

 