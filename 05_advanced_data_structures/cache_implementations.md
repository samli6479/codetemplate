# Cache Implementations (LRU & LFU)

## LRU Cache

**PSEUDOCODE:**
```
1. Initialize LRU Cache:
   - key_to_node = {} (HashMap)
   - dummyHead = new Node(0, 0)
   - dummyTail = new Node(0, 0)
   - dummyHead.next = dummyTail, dummyTail.prev = dummyHead
   - capacity = given_capacity

2. GET(key):
   a. IF key not in key_to_node: return -1
   b. node = key_to_node[key]
   c. MOVE_TO_FRONT(node)
   d. return node.value

3. PUT(key, value):
   a. IF capacity == 0: return
   b. IF key exists:
      - node = key_to_node[key]
      - node.value = value
      - MOVE_TO_FRONT(node)
      - return
   c. IF size >= capacity: EVICT_LRU()
   d. Create new_node(key, value)
   e. key_to_node[key] = new_node
   f. ADD_TO_FRONT(new_node)
   g. size++

4. MOVE_TO_FRONT(node):
   a. REMOVE_NODE(node)
   b. ADD_TO_FRONT(node)

5. EVICT_LRU():
   a. lru_node = dummyTail.prev
   b. REMOVE_NODE(lru_node)
   c. delete key_to_node[lru_node.key]
   d. size--
```

**TIME:** O(1) for get and put, **SPACE:** O(capacity)

---

## LFU Cache

**PSEUDOCODE:**
```
1. Initialize LFU Cache:
   - key_to_node = {} (HashMap)
   - freq_to_nodes = {} (HashMap of frequency → DoublyLinkedList)
   - min_freq = 0
   - capacity = given_capacity

2. GET(key):
   a. IF key not in key_to_node: return -1
   b. node = key_to_node[key]
   c. UPDATE_FREQUENCY(node)
   d. return node.value

3. PUT(key, value):
   a. IF capacity == 0: return
   b. IF key exists:
      - node = key_to_node[key]
      - node.value = value
      - UPDATE_FREQUENCY(node)
      - return
   c. IF size >= capacity: EVICT_LFU()
   d. Create new_node(key, value, freq=1)
   e. key_to_node[key] = new_node
   f. freq_to_nodes[1].add_to_front(new_node)
   g. size++, min_freq = 1

4. UPDATE_FREQUENCY(node):
   a. old_freq = node.freq
   b. new_freq = old_freq + 1
   c. freq_to_nodes[old_freq].remove_node(node)
   d. IF freq_to_nodes[old_freq].is_empty() AND old_freq == min_freq:
      - min_freq = new_freq
   e. node.freq = new_freq
   f. freq_to_nodes[new_freq].add_to_front(node)

5. EVICT_LFU():
   a. lfu_list = freq_to_nodes[min_freq]
   b. evicted_node = lfu_list.remove_last()
   c. delete key_to_node[evicted_node.key]
   d. size--
```

**TIME:** O(1) for get and put, **SPACE:** O(capacity)

---

## Doubly Linked List Operations

**PSEUDOCODE:**
```
1. ADD_TO_FRONT(node):
   a. prevHead = dummyHead.next
   b. node.next = prevHead
   c. node.prev = dummyHead
   d. prevHead.prev = node
   e. dummyHead.next = node

2. REMOVE_NODE(node):
   a. prevNode = node.prev
   b. nextNode = node.next
   c. prevNode.next = nextNode
   d. nextNode.prev = prevNode
``` 