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

> **Automatically creates missing keys.**

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



```
from collections import defaultdict

# Group values
groups = defaultdict(list)
groups[key].append(value)

# Count frequencies
count = defaultdict(int)
count[x] += 1

# Store unique values
graph = defaultdict(set)
graph[u].add(v)

# Nested dictionary
nested = defaultdict(dict)
nested[a][b] = value
```


### Common Uses

- Counting
- Grouping
- Graph adjacency list

---

# 3. deque

Double Ended Queue (pronounced "deck").
**it allows O(1) insertion and deletion from both ends.**

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
len(q)             # Size
q.clear()
q.extend([4,5])        # Adds multiple elements to the right.
q.extendleft([7,8])    # Adds multiple elements to the left in reverse order.
    output : deque([8,7,1,2])
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


- Binary Tree Level Order Traversal
- Graph Traversal
- Shortest Path in an Unweighted Graph
- Rotting Oranges
- Number of Islands
- Word Ladder
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
- Merge K Sorted Lists : Tasks with higher priority are processed first.
      - heapq.heappush(heap, (priority, task))
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
sorted(nums, key=lambda x: (x[0], x[1]))
```

Difference

```
sort()      -> modifies list  -> Works only on lists

sorted()    -> returns new list -> Works on any iterable (list, tuple, string, etc.)
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

## Initialize with the same value

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

==============
### Quick Syntax : 
==============

## 1. String Patterns

``` python
Task            Pattern                       Complexity
--------------  --------------------------   ------------
Reverse         `s[::-1]`                     O(n)
Palindrome      `s==s[::-1]`                  O(n)
Reverse words   `" ".join(s.split()[::-1])`   O(n)
Count words     `len(s.split())`              O(n)
Remove spaces   `s.replace(" ","")`           O(n)
Anagram         `Counter(a)==Counter(b)`      O(n)
```

``` python
from collections import Counter
freq=Counter("banana")
```

Common questions: 
- Reverse string
- Count vowels
- First unique
- character - Character frequency - Longest word - Remove special
- characters (`re.sub`)

## 2. List Patterns

``` python
# Remove duplicates preserving order
seen=set(); out=[]
for x in nums:
    if x not in seen:
        seen.add(x); out.append(x)
```

``` python
# Move zeros
nz=[x for x in nums if x!=0]
ans=nz+[0]*(len(nums)-len(nz))
```

``` python
# Flatten
[x for row in arr for x in row]
```

Other patterns: 
- Rotate: `nums[-k:]+nums[:-k]`
- Max/Min: `max(), min()` - Second largest (track two vars)
- Sorting: `sorted()` vs `.sort()`

## 3. Dictionary & HashMap

``` python
freq={}
for ch in s:
    freq[ch]=freq.get(ch,0)+1
```

``` python
# Two Sum
d={}
for i,x in enumerate(nums):
    if target-x in d:
        return [d[target-x],i]
    d[x]=i
```

Know: - Counter - defaultdict - get() - items(), keys(), values() - dict
comprehension

## 4. Sets

``` python
set(a)|set(b) - Union
set(a)&set(b) - Intersection
set(a)-set(b) - Difference
```

Use sets for: - Fast lookup - Duplicate detection - Union/intersection

## 5. Built-ins

-   enumerate
-   zip
-   sorted / sort
-   reversed
-   any / all
-   sum, min, max
-   map, filter
-   list, tuple, set, dict
-   append, extend, insert, pop, remove
-   split, join, strip, replace, find, count

## 6. Top Interview Questions

1.  Reverse String → slicing
2.  Palindrome → compare reverse
3.  Count vowels
4.  Character frequency
5.  First non-repeating character
6.  Remove duplicates
7.  Find duplicates
8.  Second largest
9.  Move zeros
10. Reverse words
11. Count words
12. Anagram
13. Intersection
14. Union
15. Difference
16. Flatten nested list
17. Rotate array
18. Two Sum
19. Merge dictionaries
20. Sort dictionary by value
21. List comprehensions
22. Even/Odd filtering
23. Squares/Cubes
24. Remove duplicates from sorted array
25. Basic recursion (factorial/fibonacci)

## 7. Complexity

  Operation           Time
  ------------------- ------------
  List append         O(1)
  List insert front   O(n)
  Lookup dict/set     O(1)
  Sort                O(n log n)
  Reverse slicing     O(n)

## 8. Python Tricks

``` python
nums[::-1]
sorted(nums,key=len)
max(words,key=len)
zip(*matrix)
''.join(chars)
list(map(int,input().split()))
[x*x for x in nums]
```

## 9. Common Mistakes

``` python
# Wrong
print(nums.sort())
# Right
nums.sort(); print(nums)
```

``` python
# Wrong
a=[[0]*3]*3
# Right
a=[[0]*3 for _ in range(3)]
```
----

## 10. Questions :


Q1 Reverse a String :
```python
def reverse_string(s):
    return s[::-1]
or

''.join(reversed(s))
```


Q2 Count vowels
```python
def count_vowels(s):
    vowels = set("aeiouAEIOU")
    count = 0

    for ch in s:
        if ch in vowels:
            count += 1

    return count
```

Q3 Check palindrome
```python
def palindrome(s):
    return s == s[::-1]
```


Q4 Remove duplicates from list
```python
* If order doesn't matter:
    list(set(nums))

* If order matters:
    def remove_duplicates(nums):
        seen = set()
        ans = []
    
        for x in nums:
            if x not in seen:
                seen.add(x)
                ans.append(x)
    
        return ans
```


Q5 Find maximum element
```python
max(nums)

Without max():

m = nums[0]

for x in nums:
    if x > m:
        m = x

print(m)
```



Q6 Character frequency
```python
from collections import Counter

Counter(s)
```


Q7 First non-repeating character
```python
from collections import Counter

def first_unique(s):
    c = Counter(s)

    for ch in s:
        if c[ch] == 1:
            return ch

    return None
```

Q8 Find duplicates
```python
seen = set()
dup = []

for x in nums:
    if x in seen:
        dup.append(x)
    else:
        seen.add(x)
```


Q9 Second largest
```python
first = second = float("-inf")

for x in nums:
    if x > first:
        second = first
        first = x

    elif first > x > second:
        second = x
```
----

Q10 Move all zeros to end
```python
def move_zero(nums):
    result = []

    count = 0

    for x in nums:
        if x != 0:
            result.append(x)
        else:
            count += 1

    result.extend([0] * count)

    return result
```



Q11 Reverse words
```python
" ".join(s.split()[::-1])
```


Q12 Count words
```python
len(s.split())
```


Q13 Remove spaces
```python
s.replace(" ", "")
```

Q14 Remove special characters
```python
import re
re.sub(r'[^A-Za-z0-9]', '', s)
```

Q15 Check anagram
```python
sorted(a) == sorted(b)

Better :

from collections import Counter
Counter(a) == Counter(b)
```
----

Lists :
```python
Q16 Lists Intersection
    - list(set(a) & set(b))

Q17 Lists Union
    - list(set(a) | set(b))

Q18 Lists Difference
    - list(set(a) - set(b))

Q19 Lists Flatten
    - res = [x for row in nums for x in row]

Q20 Rotate Lists by k 
    - nums[-k:] + nums[:-k]

List Comprehensions:

Even numbers
    - [x for x in nums if x % 2 == 0]
Squares
    - [x*x for x in nums]
Dictionary
    - {x: x*x for x in nums}
```

----

Q21 Invert dictionary
```python
d = {'a':1,'b':2}

{v:k for k,v in d.items()}
```

Q22 Merge dictionaries
```python
d1 | d2

or 

{**d1, **d2}
```


Q23 Sort dictionary by value
```python
sorted(d.items(), key=lambda x: x[1])
```
----

Q : transpose of a matrix
```python
matrix = [
    [1, 2],
    [3, 4],
    [5, 6]
]

# zip(*matrix) groups column elements; map() converts resulting tuples back to lists
transposed = list(map(list, zip(*matrix)))

OR

# Outer loop tracks column count, inner loop tracks row count
transposed = [[row[i] for row in matrix] for i in range(len(matrix[0]))]

OR

# Transpose using .T
import numpy as np

matri_new = np.array(matrix)
transposed = matrix.T


print(transposed)
# Output: [[1, 3, 5], [2, 4, 6]]
```



Two-Pointer Questions :

Q24 Two Sum
```python
def twoSum(arr, target):
  
    # Create a set to store the elements
    s = set()
    for num in arr:
        # Calculate the complement that added to
        # num, equals the target
        complement = target - num

        # Check if the complement exists in the set
        if complement in s:
            return True

        # Add the current element to the set
        s.add(num)

    # If no pair is found
    return False
```

Q25 Remove duplicates (sorted array)
```python
i = 0

for j in range(1, len(nums)):
    if nums[j] != nums[i]:
        i += 1
        nums[i] = nums[j]

return i + 1
```


-----




