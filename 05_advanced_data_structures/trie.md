# Trie

**PSEUDOCODE:**
```
1. Define TrieNode class:
   - children = {}  # Dictionary mapping char to child node
   - is_end = False # Marks end of a word

2. Insert(word):
   a. current = root
   b. FOR each char in word:
      - IF char not in current.children: 
        * current.children[char] = TrieNode()
      - current = current.children[char]
   c. current.is_end = True

3. Search(word):
   a. current = root
   b. FOR each char in word:
      - IF char not in current.children: return False
      - current = current.children[char]
   c. Return current.is_end

4. StartsWith(prefix):
   a. current = root
   b. FOR each char in prefix:
      - IF char not in current.children: return False
      - current = current.children[char]
   c. Return True
```

**DETAILED STEPS:**
- **Node structure**: Each node has children dict and end flag
- **Insertion**: Traverse/create path, mark end node
- **Search**: Traverse path, check if end node exists
- **Prefix**: Traverse path, don't check end flag
- **Memory**: Shared prefixes save space

**TIME:** O(m) per operation, **SPACE:** O(m*n) where m is word length  
**USE:** Word dictionary, prefix matching, autocomplete 