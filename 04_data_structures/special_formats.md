# Special String Format Patterns

## 1. Roman Numeral Conversion

**PSEUDOCODE:**
```
1. Initialize roman_map = {'I':1, 'V':5, 'X':10, 'L':50, 'C':100, 'D':500, 'M':1000}
2. Initialize result = 0, prev = 0
3. FOR i from n-1 to 0:
   a. current = roman_map[s[i]]
   b. IF current >= prev: result += current
   c. ELSE: result -= current
   d. prev = current
4. Return result
```

**TIME:** O(n), **SPACE:** O(1)  
**USE:** Roman to integer conversion

**EXAMPLE:**
```
"III" → 3
"IV" → 4
"IX" → 9
"LVIII" → 58
"MCMXCIV" → 1994
```

---

## 2. Integer to Roman

**PSEUDOCODE:**
```
1. Initialize roman_symbols = [(1000,'M'), (900,'CM'), (500,'D'), (400,'CD'), 
                              (100,'C'), (90,'XC'), (50,'L'), (40,'XL'),
                              (10,'X'), (9,'IX'), (5,'V'), (4,'IV'), (1,'I')]
2. Initialize result = ""
3. FOR each (value, symbol) in roman_symbols:
   a. WHILE num >= value:
      - result += symbol
      - num -= value
4. Return result
```

**TIME:** O(1), **SPACE:** O(1)  
**USE:** Integer to Roman conversion

**EXAMPLE:**
```
3 → "III"
4 → "IV"
9 → "IX"
58 → "LVIII"
1994 → "MCMXCIV"
```

---

## 3. Valid Parentheses with Multiple Types

**PSEUDOCODE:**
```
1. Initialize stack = [], pairs = {')':'(', '}':'{', ']':'['}
2. FOR each character in string:
   a. IF char is opening: push to stack
   b. IF char is closing:
      - IF stack empty OR stack.pop() != pairs[char]: return false
3. Return stack is empty
```

**TIME:** O(n), **SPACE:** O(n)  
**USE:** Valid parentheses with mixed brackets

**EXAMPLE:**
```
"()[]{}" → true
"([)]" → false
"{[]}" → true
"(((" → false
```

---

## 4. String Compression (In-Place)

**PSEUDOCODE:**
```
1. Initialize write_pos = 0, count = 1
2. FOR i from 1 to n:
   a. IF s[i] == s[i-1]: count++
   b. ELSE:
      - s[write_pos] = s[i-1], write_pos++
      - IF count > 1: write count as string
      - count = 1
3. Handle last group
4. Return write_pos
```

**TIME:** O(n), **SPACE:** O(1)  
**USE:** String compression in-place

**EXAMPLE:**
```
["a","a","b","b","c","c","c"] → ["a","2","b","2","c","3"]
["a"] → ["a"]
["a","b","b","b","b","b","b","b","b","b","b","b","b"] → ["a","b","1","2"]
```

**KEY INSIGHTS:**
- **Roman numerals**: Process right to left, subtract when smaller
- **Integer to Roman**: Use predefined symbol-value pairs
- **Multiple parentheses**: Use hash map for bracket pairs
- **In-place compression**: Use write pointer to overwrite array

---

## 5. String Compression (Character Count)

**PSEUDOCODE:**
```
1. Initialize result = [], count = 1, current_char = s[0]
2. FOR i from 1 to n-1:
   a. IF s[i] == current_char: count++
   b. ELSE:
      - result.append(current_char)
      - IF count > 1: result.append(str(count))
      - current_char = s[i], count = 1
3. result.append(current_char)
4. IF count > 1: result.append(str(count))
5. Return ''.join(result)
```

**TIME:** O(n), **SPACE:** O(n)  
**USE:** String compression, character counting

**EXAMPLE:**
```
"aaabbc" → "a3b2c1"
"abc" → "abc"
"aabbb" → "a2b3"
``` 