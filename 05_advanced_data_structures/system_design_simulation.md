# System Design Simulation Patterns

## 1. TTL (Time-To-Live) Cache

**PSEUDOCODE:**
```
1. Initialize TTL Cache:
   - data_store = {}  # key -> (value, expiration_time)
   - current_time = 0

2. SET(key, value, ttl):
   a. expiration_time = current_time + ttl
   b. data_store[key] = (value, expiration_time)

3. GET(key):
   a. IF key not in data_store: return -1
   b. (value, expiration_time) = data_store[key]
   c. IF current_time > expiration_time:
      - delete data_store[key]
      - return -1
   d. return value

4. RENEW(key, current_time):
   a. IF key not in data_store: return false
   b. (value, old_expiration) = data_store[key]
   c. IF current_time > old_expiration: return false
   d. new_expiration = current_time + ttl
   e. data_store[key] = (value, new_expiration)
   f. return true

5. COUNT_UNEXPIRED(current_time):
   a. count = 0
   b. FOR each (key, (value, expiration_time)) in data_store:
      - IF current_time <= expiration_time:
        * count++
   c. return count
```

**TIME:** O(1) for get/set/renew, O(n) for count, **SPACE:** O(n)

---

## 2. Debounce Function

**PSEUDOCODE:**
```
1. Initialize debounce function:
   - timeout_id = null
   - delay = given_delay

2. DEBOUNCE_FUNCTION():
   a. IF timeout_id exists:
      - clearTimeout(timeout_id)
   b. timeout_id = setTimeout(execute_function, delay)

3. EXECUTE_FUNCTION():
   a. Perform the actual function call
   b. timeout_id = null
```

**TIME:** O(1) per call, **SPACE:** O(1)

---

## 3. Throttle Function

**PSEUDOCODE:**
```
1. Initialize throttle function:
   - last_execution = 0
   - delay = given_delay

2. THROTTLE_FUNCTION():
   a. current_time = getCurrentTime()
   b. IF current_time - last_execution >= delay:
      - execute_function()
      - last_execution = current_time
```

**TIME:** O(1) per call, **SPACE:** O(1)

---

## 4. Rate Limiter

**PSEUDOCODE:**
```
1. Initialize rate limiter:
   - requests = []  # Store timestamps
   - max_requests = given_limit
   - window_size = given_window

2. REQUEST():
   a. current_time = getCurrentTime()
   b. CLEANUP_OLD_REQUESTS(current_time)
   c. IF len(requests) < max_requests:
      - requests.append(current_time)
      - return true
   d. return false

3. CLEANUP_OLD_REQUESTS(current_time):
   a. WHILE requests and requests[0] <= current_time - window_size:
      - requests.pop(0)
```

**TIME:** O(1) amortized, **SPACE:** O(max_requests) 