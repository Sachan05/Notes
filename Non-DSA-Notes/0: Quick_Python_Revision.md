# Python Interview Revision Sheet (Collections & Built-in Utilities)

> **Goal:** 15-minute revision before a coding assessment (CodeSignal / LeetCode / Interviews)

---

# 1. Counter (Frequency Counting)

```python
from collections import Counter

nums = [1,2,2,3,3,3]

cnt = Counter(nums)

print(cnt)
# Counter({3:3, 2:2, 1:1})
```

### Most Common Operations

```python
cnt[x] += 1            # Increment frequency
cnt[x] -= 1            # Decrement frequency
cnt[x]                 # Get frequency (0 if missing)
cnt.items()            # (element, count)
cnt.keys()             # Elements
cnt.values()           # Counts
cnt.most_common(1)     # Most frequent
cnt.most_common(3)     # Top 3 frequent
```

### Common Uses

- Frequency counting
- Duplicate detection
- Character counting
- Most frequent element

Example

```python
Counter("banana")
# {'a':3, 'n':2, 'b':1}
```

---

# 2. defaultdict

Automatically creates missing keys.

```python
from collections import defaultdict
```

## Counting

```python
count = defaultdict(int)

count[5] += 1
count[5] += 1

print(count)
# {5:2}
```

## Grouping

```python
groups = defaultdict(list)

groups["Math"].append("Alice")
groups["Math"].append("Bob")
```

Output

```python
{
    "Math": ["Alice", "Bob"]
}
```

## Other Useful Types

```python
defaultdict(int)      # default = 0
defaultdict(list)     # default = []
defaultdict(set)      # default = set()
defaultdict(dict)     # default = {}
```

### Common Uses

- Counting
- Grouping
- Graph adjacency list

---

# 3. deque

Double Ended Queue

```python
from collections import deque

q = deque()
```

### Operations

```python
q.append(x)        # Right
q.appendleft(x)    # Left

q.pop()            # Remove right
q.popleft()        # Remove left

q[0]               # Front
q[-1]              # Back
```

### Queue (FIFO)

```python
q.append(1)
q.append(2)

q.popleft()
```

### Stack (LIFO)

```python
q.append(1)
q.append(2)

q.pop()
```

### Used In

- BFS
- Sliding Window
- Queue
- Stack

---

# 4. Heap (Priority Queue)

```python
import heapq

heap = []
```

## Min Heap (Default)

```python
heapq.heappush(heap, x)

smallest = heapq.heappop(heap)

peek = heap[0]
```

## Max Heap

```python
heapq.heappush(heap, -x)

largest = -heapq.heappop(heap)
```

### Used In

- K largest/smallest
- Priority Queue
- Merge K Sorted Lists
- Scheduling

Complexity

```
Push -> O(log n)

Pop -> O(log n)

Peek -> O(1)
```

---

# 5. Sorting

## Ascending

```python
nums.sort()
```

## Descending

```python
nums.sort(reverse=True)
```

## Sort by Length

```python
words.sort(key=len)
```

## Sort by One Field

```python
arr.sort(key=lambda x: x[1])
```

Example

```python
students = [
    ("Alice",85),
    ("Bob",92)
]

students.sort(key=lambda x:x[1])
```

## Multiple Keys

```python
arr.sort(key=lambda x:(x[0], x[1]))
```

## First Ascending, Second Descending

```python
arr.sort(key=lambda x:(x[0], -x[1]))
```

## New Sorted List

```python
new = sorted(arr)
```

Difference

```
sort()      -> modifies list

sorted()    -> returns new list
```

---

# 6. enumerate()

Returns index + value.

```python
nums = [10,20,30]

for i, x in enumerate(nums):
    print(i, x)
```

Output

```
0 10

1 20

2 30
```

Start from 1

```python
for i, x in enumerate(nums, start=1):
    ...
```

Used when both index and value are needed.

---

# 7. zip()

Iterate over multiple iterables together.

```python
A = [1,2,3]
B = ['a','b','c']

for a,b in zip(A,B):
    print(a,b)
```

Output

```
1 a

2 b

3 c
```

## Build Dictionary

```python
keys = ["name","age"]

values = ["Alice",25]

d = dict(zip(keys, values))
```

## Unzip

```python
pairs = [(1,'a'), (2,'b')]

A, B = zip(*pairs)
```

## Matrix Transpose

```python
transpose = list(zip(*matrix))
```

---

# 8. Reverse String / List

```python
s[::-1]
```

Example

```python
"hello"[::-1]

# olleh
```

Works for lists too

```python
nums[::-1]
```

Palindrome

```python
if s == s[::-1]:
    print("Palindrome")
```

---

# 9. join()

Convert list of strings into one string.

```python
arr = ["H","e","l","l","o"]

"".join(arr)

# Hello
```

With separator

```python
" ".join(words)

",".join(arr)

"-".join(arr)
```

Integers

```python
"".join(map(str, nums))
```

---

# 10. split()

Convert string into list.

```python
s = "I love Python"

words = s.split()
```

Output

```python
['I','love','Python']
```

Custom separator

```python
s.split(",")

date.split("-")
```

Useful for parsing input.

---

# 11. set()

Stores unique values.

```python
seen = set()
```

Operations

```python
seen.add(x)

x in seen

seen.remove(x)

len(seen)
```

Duplicate Detection

```python
seen = set()

for x in nums:

    if x in seen:
        print("Duplicate")

    seen.add(x)
```

Remove duplicates

```python
unique = list(set(nums))
```

Lookup

```
Set  -> O(1)

List -> O(n)
```

---

# 12. List Initialization

## Initialize with same value

```python
ans = [1] * n
```

Example

```python
n = 5

ans = [1]*n

# [1,1,1,1,1]
```

Also

```python
visited = [False]*n

dp = [0]*n
```

Very common in DP and Prefix/Suffix problems.

---

# Most Important Time Complexities

| Operation | Complexity |
|-----------|------------|
| List append | O(1) |
| List pop() | O(1) |
| List pop(0) | O(n) |
| deque append | O(1) |
| deque popleft | O(1) |
| Set lookup | O(1) |
| Dict lookup | O(1) |
| Counter lookup | O(1) |
| Heap push/pop | O(log n) |
| Sorting | O(n log n) |
| String reverse | O(n) |
| split() | O(n) |
| join() | O(n) |

---

# Python Cheat Sheet (Memorize)

```python
from collections import Counter, defaultdict, deque
import heapq

# Counter
cnt = Counter(nums)
cnt[x] += 1
cnt.most_common(1)

# defaultdict
d = defaultdict(list)
d[key].append(value)

count = defaultdict(int)
count[x] += 1

# deque
q = deque()
q.append(x)
q.appendleft(x)
q.pop()
q.popleft()

# Heap
heap = []
heapq.heappush(heap, x)
smallest = heapq.heappop(heap)

# Max Heap
heapq.heappush(heap, -x)
largest = -heapq.heappop(heap)

# Sorting
nums.sort()
nums.sort(reverse=True)
nums.sort(key=len)
nums.sort(key=lambda x: x[1])
nums.sort(key=lambda x: (x[0], -x[1]))
new = sorted(nums)

# enumerate
for i, x in enumerate(nums):
    ...

# zip
for a, b in zip(A, B):
    ...

# Reverse
s[::-1]

# Join
"".join(arr)

# Split
s.split()

# Set
seen = set()
seen.add(x)
if x in seen:
    ...

# List Initialization
ans = [1] * n
visited = [False] * n
dp = [0] * n
```

---

# 🚀 High-Frequency Interview Patterns

| Pattern | Tool |
|---------|------|
| Frequency Count | `Counter`, `defaultdict(int)` |
| Group Elements | `defaultdict(list)` |
| Remove Duplicates | `set()` |
| Fast Lookup | `set()`, `dict` |
| Queue / BFS | `deque` |
| Stack | `list` or `deque` |
| Sliding Window | `deque` |
| Priority Queue | `heapq` |
| K Largest / Smallest | `heapq` |
| Index + Value | `enumerate()` |
| Iterate Two Lists | `zip()` |
| Reverse String | `[::-1]` |
| Convert List → String | `"".join()` |
| Convert String → List | `split()` |
| Multi-Key Sorting | `key=lambda` |
| Prefix / DP Arrays | `[1]*n`, `[0]*n`, `[False]*n` |

---

## ⭐ If you can comfortably use every pattern on this sheet without looking it up, you'll be well prepared for most Python-based coding assessments (CodeSignal, LeetCode Easy/Medium, HackerRank, etc.).
