# LeetCode 150 — Beginner's Guide to Data Structures & Algorithms in Python

Welcome! This guide is written for someone new to data structures and algorithms. Every concept starts with a **real-world analogy**, walks through a **concrete example step-by-step**, and explains **why the code works** — not just what it does.

---

## How to Read This Guide

Each section follows the same structure:
1. **What is it?** — plain-English explanation
2. **Real-world analogy** — something from daily life
3. **When to use it** — the signals in a problem
4. **Walkthrough example** — code with a trace
5. **Complexity explained** — why it's fast or slow
6. **Common mistakes** — what beginners get wrong

---

## Table of Contents

**Foundations**
- [Understanding Complexity (Big O)](#understanding-complexity-big-o)

**Part 1: Array & String Techniques**
- [1. Array / String Basics](#1-array--string-basics)
- [2. Two Pointers](#2-two-pointers)
- [3. Sliding Window](#3-sliding-window)
- [4. Matrix](#4-matrix)
- [5. Hashmap](#5-hashmap)
- [6. Intervals](#6-intervals)

**Part 2: Linear Data Structures**
- [7. Stack](#7-stack)
- [8. Linked List](#8-linked-list)

**Part 3: Trees**
- [9. Binary Tree — DFS](#9-binary-tree--dfs-depth-first-search)
- [10. Binary Tree — BFS](#10-binary-tree--bfs-breadth-first-search)
- [11. Binary Search Tree](#11-binary-search-tree-bst)
- [14. Trie](#14-trie-prefix-tree)

**Part 4: Graphs**
- [12. Graph — DFS](#12-graph--dfs)
- [13. Graph — BFS](#13-graph--bfs)

**Part 5: Search & Optimization**
- [15. Backtracking](#15-backtracking)
- [16. Divide and Conquer](#16-divide-and-conquer)
- [18. Binary Search](#18-binary-search)
- [19. Heap (Priority Queue)](#19-heap-priority-queue)

**Part 6: Dynamic Programming**
- [17. Kadane's Algorithm](#17-kadanes-algorithm)
- [22. 1D Dynamic Programming](#22-1d-dynamic-programming)
- [23. Multi-D Dynamic Programming](#23-multi-d-dynamic-programming)

**Part 7: Misc**
- [20. Bit Manipulation](#20-bit-manipulation)
- [21. Math](#21-math)

**Appendix**
- [Python Cheatsheet for Beginners](#python-cheatsheet-for-beginners)

---

## Understanding Complexity (Big O)

Before we start, you need to understand **why we care about complexity**. Let's use a real story.

### The story
Imagine you own a phonebook business. You have 1 million contacts. Someone asks: "What's John's phone number?"

- **Approach A**: Flip through pages one by one until you find John. If John is on the last page, you check 1 million entries.
- **Approach B**: Since names are sorted, open to the middle. Is "John" before or after the middle name? Throw away half. Repeat. You'll find John in about 20 steps.

Both work. But Approach A takes hours; Approach B takes seconds. That's **complexity**.

### Big O Notation

Big O tells you **how the number of operations grows as input size grows**. We use `n` for the input size.

| Notation     | Name          | Rough meaning                       | Example for n = 1,000,000     |
|--------------|---------------|-------------------------------------|-------------------------------|
| O(1)         | Constant      | Same time no matter the input       | 1 step                        |
| O(log n)     | Logarithmic   | Doubling n adds one step            | ~20 steps                     |
| O(n)         | Linear        | Time grows with n                   | 1,000,000 steps               |
| O(n log n)   | Linearithmic  | Slightly worse than linear          | ~20,000,000 steps             |
| O(n²)        | Quadratic     | Nested loops                        | 1,000,000,000,000 steps 💀    |
| O(2ⁿ)        | Exponential   | Doubling each step                  | Universe won't finish 💀💀     |

### Why the difference matters

If a computer does 100 million operations per second:
- O(n) with n = 1,000,000 → **0.01 seconds** ✅
- O(n²) with n = 1,000,000 → **~3 hours** ❌
- O(n log n) with n = 1,000,000 → **~0.2 seconds** ✅

**Rule of thumb: aim for O(n log n) or better.**

### Space complexity
Same idea, but for **memory** instead of time. If you make a copy of the input, you use O(n) extra space. If you use a few variables, that's O(1) space.

---

## 1. Array / String Basics

### What is it?
An **array** (called `list` in Python) is a numbered collection of items stored side-by-side in memory. A **string** is like an array of characters, but you can't change individual characters in Python.

```python
groceries = ["milk", "bread", "eggs", "cheese"]
#             0        1        2        3
```

### Real-world analogy
Think of a **row of numbered mailboxes** in an apartment building. Each mailbox has an address (0, 1, 2, ...) and holds one item. To get the item in mailbox 2, you walk directly to mailbox 2 — you don't need to open the others.

### Key idea: instant access, slow insertion in the middle
- **Getting `groceries[2]`** → instant. You know exactly where mailbox 2 is. **O(1)**.
- **Inserting "butter" at position 1** → slow. You'd have to shift "bread", "eggs", and "cheese" one mailbox down to make room. **O(n)**.

### Real-world scenario: attendance list
Your teacher has a list of 30 students. She wants to:
1. Check who's in seat #5 → instant (O(1)).
2. Add a new student at the end → instant (O(1)).
3. Insert a new student alphabetically in the middle → slow, everyone after has to shuffle down (O(n)).

### The string trap (very important for Python beginners!)

Strings in Python are **immutable** — you can't change them. Every time you "add to" a string, Python secretly creates a brand new one.

**Bad code (slow):**
```python
result = ""
for word in ["Hello", "World", "!"]:
    result = result + word    # creates a NEW string each time
```
This is O(n²) — for 10,000 words, it's 100 million operations!

**Good code (fast):**
```python
result = "".join(["Hello", "World", "!"])
```
This is O(n) — for 10,000 words, it's 10,000 operations. **10,000x faster.**

### Walkthrough example: Remove duplicates from a sorted list

**Problem**: Given `[1, 1, 2, 2, 3]`, modify it in place so it becomes `[1, 2, 3, _, _]` and return 3 (the new length).

**Key idea**: use a "write pointer". Only advance the write pointer when we see a new value.

```python
def remove_duplicates(nums):
    if not nums:
        return 0
    
    write = 1  # position where next unique value will go
    
    for read in range(1, len(nums)):
        if nums[read] != nums[read - 1]:  # found a new value
            nums[write] = nums[read]
            write += 1
    
    return write
```

**Trace with `[1, 1, 2, 2, 3]`**:

| read | nums[read] | nums[read-1] | New value? | write before | Action           | Array state      |
|------|------------|--------------|------------|--------------|------------------|------------------|
| 1    | 1          | 1            | No         | 1            | skip             | [1,1,2,2,3]      |
| 2    | 2          | 1            | Yes        | 1            | write nums[1]=2  | [1,2,2,2,3]      |
| 3    | 2          | 2            | No         | 2            | skip             | [1,2,2,2,3]      |
| 4    | 3          | 2            | Yes        | 2            | write nums[2]=3  | [1,2,3,2,3]      |

Return 3. The first 3 elements are the unique values.

### Complexity in detail
- **Time**: We look at each element exactly once. If there are n elements, we do n operations. That's **O(n)**.
- **Space**: We use two variables (`write`, `read`) no matter how big the array is. That's **O(1)**.

### Common beginner mistakes
1. **`[[0] * 3] * 3` for 2D lists** — this creates a list of 3 references to the SAME inner list! Modifying one row modifies all rows.
   ```python
   bad  = [[0] * 3] * 3           # ❌ shared rows
   good = [[0] * 3 for _ in range(3)]  # ✅ separate rows
   ```
2. **Building strings with `+=` in a loop** — as shown above, use `"".join(list)` instead.
3. **Modifying a list while looping over it** — iterate over a copy, or build a new list.

---

## 2. Two Pointers

### What is it?
A technique where you use **two indices** (pointers) moving through the array in a coordinated way. This lets us solve in O(n) what would take O(n²) with nested loops.

### Real-world analogy
Imagine you're **searching a sorted bookshelf** for two books whose combined thickness equals exactly 5 cm. You have a shortcut: place one hand at the leftmost book (thinnest) and one at the rightmost (thickest).

- If their combined thickness is too small → move the LEFT hand right (add a thicker book).
- If too big → move the RIGHT hand left (try a thinner book).
- If exactly 5 → found it!

You never need to compare every pair. You just walk the two hands toward each other.

### Three patterns

**Pattern A: Opposite ends** (start from both ends, move toward middle)
Used for: two-sum on sorted array, checking palindromes, container with most water.

**Pattern B: Same direction (fast/slow)** (both start at the beginning, one moves faster)
Used for: removing elements, cycle detection.

**Pattern C: Fixed gap** (both start together, one stays ahead by k)
Used for: finding the k-th element from the end.

### Real-world scenario: Checking a palindrome
Is "racecar" a palindrome? Point one finger at 'r' (left) and another at 'r' (right). Same → move both inward. Do 'a' and 'a' match? Move inward. Do 'c' and 'c' match? Yes. Eventually pointers meet — it IS a palindrome.

```python
def is_palindrome(s):
    left, right = 0, len(s) - 1
    while left < right:
        if s[left] != s[right]:
            return False
        left += 1
        right -= 1
    return True

print(is_palindrome("racecar"))  # True
print(is_palindrome("hello"))    # False
```

### Walkthrough example: Two Sum on a sorted array

**Problem**: Given a sorted list `[2, 7, 11, 15]` and a target `9`, find two numbers that add up to 9.

```python
def two_sum(nums, target):
    left, right = 0, len(nums) - 1
    while left < right:
        current_sum = nums[left] + nums[right]
        if current_sum == target:
            return [left, right]
        elif current_sum < target:
            left += 1   # need bigger sum, so move left right
        else:
            right -= 1  # need smaller sum, so move right left
    return []
```

**Trace with `[2, 7, 11, 15]`, target = 9**:

| Step | left | right | nums[left] + nums[right] | Compare to 9 | Action             |
|------|------|-------|--------------------------|--------------|--------------------|
| 1    | 0    | 3     | 2 + 15 = 17              | too big      | right -= 1         |
| 2    | 0    | 2     | 2 + 11 = 13              | too big      | right -= 1         |
| 3    | 0    | 1     | 2 + 7  = 9               | match! ✅    | return [0, 1]      |

### Complexity in detail

**Why is this O(n) and not O(n²)?**

- With nested loops (brute force), you'd try every pair: `for i in range(n): for j in range(i+1, n): ...` That's `n × n / 2` pairs = **O(n²)**.
- With two pointers, each pointer moves at most n times, and they always move toward each other. Total moves: at most n. That's **O(n)**.

For n = 1,000,000:
- Brute force: 500 billion operations → hours
- Two pointers: 1 million operations → 0.01 seconds

**Space**: We use two variables. **O(1)**.

### Common beginner mistakes
1. **Forgetting the array must be sorted** — two pointers usually rely on order.
2. **Using `while left <= right`** — if the problem says "two DIFFERENT elements", use `<` so you never pair an element with itself.
3. **Forgetting to move the pointer** — infinite loop!

---

## 3. Sliding Window

### What is it?
A special two-pointer technique for finding a **contiguous** (side-by-side) chunk of an array or string that satisfies some condition. Think of a window sliding across the data.

### Real-world analogy
Imagine you're driving a car and looking through the **windshield** at a 5-car stretch of the highway ahead. As you drive forward, one new car enters your view on the right, and one old car leaves on the left. You never re-examine cars you've already seen.

Another analogy: you're watching a movie through a **rectangular slot** on a moving strip. The slot has fixed width. As the strip moves, new content enters one side and old content exits the other.

### Two types

**Fixed-size window**: the window is always exactly `k` wide.
Example: "average temperature of the last 7 days" — the window is always 7.

**Variable-size window**: the window grows and shrinks based on a condition.
Example: "longest stretch of days without rain" — the window grows as long as no rain, shrinks (starts over) when it rains.

### Real-world scenario: rolling average of stock prices

You have daily stock prices for a year. You want the average price over each 5-day window.

**Naive approach (slow)**: for each starting day, sum the next 5 prices. That's 5 additions per day × 365 days = 1825 additions. This is O(n × k).

**Sliding window approach (fast)**: keep the sum of the current 5 days. When moving one day forward, ADD the new day, SUBTRACT the day that left the window. That's 2 operations per day × 365 = 730 operations. This is O(n).

```python
def rolling_averages(prices, k):
    window_sum = sum(prices[:k])  # initial sum of first k days
    averages = [window_sum / k]
    
    for i in range(k, len(prices)):
        window_sum += prices[i]        # add new day
        window_sum -= prices[i - k]    # remove old day
        averages.append(window_sum / k)
    
    return averages
```

### Walkthrough example: Longest substring without repeating characters

**Problem**: In "abcabcbb", find the longest chunk where no character repeats. Answer: "abc" (length 3).

**Idea**: expand the window to the right as long as no repeats. When a repeat happens, shrink from the left until the repeat is gone.

```python
def longest_unique(s):
    seen = {}       # character -> most recent index where we saw it
    left = 0
    best = 0
    
    for right in range(len(s)):
        char = s[right]
        # If we've seen this char AND it's still inside our window
        if char in seen and seen[char] >= left:
            left = seen[char] + 1   # shrink window past the duplicate
        seen[char] = right
        best = max(best, right - left + 1)
    
    return best
```

**Trace with "abcabcbb"**:

| right | char | seen[char]? | left before | left after | Window     | Length | best |
|-------|------|-------------|-------------|------------|------------|--------|------|
| 0     | 'a'  | no          | 0           | 0          | "a"        | 1      | 1    |
| 1     | 'b'  | no          | 0           | 0          | "ab"       | 2      | 2    |
| 2     | 'c'  | no          | 0           | 0          | "abc"      | 3      | 3    |
| 3     | 'a'  | yes (0)     | 0           | 1          | "bca"      | 3      | 3    |
| 4     | 'b'  | yes (1)     | 1           | 2          | "cab"      | 3      | 3    |
| 5     | 'c'  | yes (2)     | 2           | 3          | "abc"      | 3      | 3    |
| 6     | 'b'  | yes (4)     | 3           | 5          | "cb"       | 2      | 3    |
| 7     | 'b'  | yes (6)     | 5           | 7          | "b"        | 1      | 3    |

Answer: 3.

### Complexity in detail

**Why is this O(n) even though there's a "while" or "if" inside a "for" loop?**

Think about it this way: `right` moves n times (once per character). `left` also moves at most n times total across the whole run (it only ever moves forward, never backward). So the TOTAL number of pointer moves is at most 2n. That's **O(n)**.

The mistake beginners make: they see a nested-looking structure and assume O(n²). But if the inner pointer's total work across all iterations is bounded, it's still O(n). This is called **amortized analysis**.

**Space**: The `seen` dictionary holds at most one entry per unique character. If the alphabet has 26 letters, it's O(26) = **O(1)**. For arbitrary characters, it's **O(k)** where k is the alphabet size.

### Common beginner mistakes
1. **Trying to apply sliding window when the sequence isn't contiguous** — for subsequences (not necessarily side-by-side), you need DP.
2. **Forgetting to update `left` when the condition breaks** — window grows forever.
3. **Off-by-one in window length**: it's `right - left + 1` (inclusive on both ends).

---

## 4. Matrix

### What is it?
A matrix is a **2D grid** of values — a list of lists. Each cell has a row and a column.

```python
grid = [
    [1, 2, 3],   # row 0
    [4, 5, 6],   # row 1
    [7, 8, 9]    # row 2
]
# grid[1][2] is 6 (row 1, column 2)
```

### Real-world analogy
Think of a **chess board**, an **Excel spreadsheet**, or a **city map divided into blocks**. Each cell has an address (row, column).

### Real-world scenario: image processing
An image is a matrix! Each pixel is a cell. Rotating a photo, applying filters, or scanning for edges — all involve walking through a matrix.

### Common operations you'll need

**1. Iterate every cell:**
```python
rows, cols = len(grid), len(grid[0])
for r in range(rows):
    for c in range(cols):
        print(grid[r][c])
```

**2. Visit the 4 neighbors of a cell (up, down, left, right):**
```python
for dr, dc in [(-1, 0), (1, 0), (0, -1), (0, 1)]:
    nr, nc = r + dr, c + dc
    if 0 <= nr < rows and 0 <= nc < cols:  # in bounds
        print(grid[nr][nc])
```

The `[(-1, 0), (1, 0), (0, -1), (0, 1)]` is a common trick. Each pair is a "direction": up, down, left, right. You use it any time you're walking on a grid.

### Walkthrough example: Rotate an image 90° clockwise

**Problem**: Given a matrix representing a photo, rotate it 90° clockwise in place.

```
Before:        After:
1 2 3          7 4 1
4 5 6    →     8 5 2
7 8 9          9 6 3
```

**Key insight**: rotation = transpose + reverse each row.

- **Transpose**: swap rows and columns. Position (r, c) becomes (c, r).
- **Reverse each row**: flips horizontally.

```python
def rotate(matrix):
    n = len(matrix)
    
    # Step 1: Transpose (swap across the diagonal)
    for i in range(n):
        for j in range(i + 1, n):  # only upper triangle
            matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]
    
    # Step 2: Reverse each row
    for row in matrix:
        row.reverse()
```

**After transpose**:
```
1 4 7
2 5 8
3 6 9
```

**After reversing each row**:
```
7 4 1
8 5 2
9 6 3
```

### Complexity in detail

**Time**: A matrix with n rows and n columns has n² cells. We touch each cell a constant number of times. So it's **O(n²)**.

Wait, isn't O(n²) bad? Not necessarily! Here n is the SIDE length. The total data is n × n = n² cells. Since we must touch all cells, we can't do better than O(n²) — it's O(total cells), which is optimal.

**Space**: We rotate in place — no new matrix. **O(1)** extra space.

### Common beginner mistakes
1. **Mixing up rows and columns** — always name variables clearly: `r, c` not `i, j`.
2. **Going out of bounds** — always check `0 <= r < rows and 0 <= c < cols`.
3. **Sharing inner lists**: `[[0] * cols] * rows` creates aliases, not copies!

---

## 5. Hashmap

### What is it?
A **hashmap** (Python `dict`) is a data structure that lets you look up values by key in **constant time**. It's like a super-fast dictionary.

### Real-world analogy
A **coat check** at a fancy restaurant. When you drop off your coat, you get a ticket (the key). When you come back, you show the ticket, and the attendant instantly retrieves your coat. They don't have to search through all coats — they know exactly where yours is because of your ticket number.

Another analogy: a **contacts app**. You type "Mom" and it instantly shows her number. You don't scroll through 500 contacts one by one.

### Why is it so fast?
Under the hood, a hashmap uses a **hash function** to convert your key into an address. It's like magic math that turns "Mom" into position 42. Since we go directly to position 42, lookup is O(1).

### When to use it
Any time you need to:
- **Count things**: how many times each word appears
- **Check if you've seen something before**: has this number appeared already?
- **Look up values by keys**: given a name, find the phone number
- **Group similar things together**: put all anagrams in the same bucket

### Real-world scenario: cashier with a memory

Imagine you're a cashier. Customers keep asking: "Do I have a discount code for $10?" You could rummage through a pile of codes every time (slow), OR keep them in a labeled drawer (fast). The labeled drawer is a hashmap: label → code.

### Walkthrough example: Two Sum (the classic!)

**Problem**: Given `nums = [2, 7, 11, 15]` and `target = 9`, return the indices of two numbers that add up to the target. Answer: `[0, 1]` because 2 + 7 = 9.

**Naive approach**: check every pair. O(n²).

**Hashmap approach**: as we walk through the list, remember every number we've seen. For each new number, check if the "partner" (target − current) has already been seen.

```python
def two_sum(nums, target):
    seen = {}  # value -> index
    for i, num in enumerate(nums):
        needed = target - num
        if needed in seen:
            return [seen[needed], i]
        seen[num] = i
    return []
```

**Trace with `[2, 7, 11, 15]`, target = 9**:

| i | num | needed (9 - num) | seen before? | seen dict after       | Return?       |
|---|-----|------------------|--------------|-----------------------|---------------|
| 0 | 2   | 7                | no           | {2: 0}                | keep going    |
| 1 | 7   | 2                | YES (at 0)   | —                     | return [0, 1] |

We only needed 2 steps for this small example. For 1000 numbers, we'd do 1000 steps instead of 500,000.

### Real-world scenario: anagram grouping

You have a bag of Scrabble tiles. You want to group words that use the same letters together: "eat", "tea", "ate" all go in one group.

**Key insight**: two words are anagrams if their sorted characters are equal. So use the sorted string as a dictionary key!

```python
from collections import defaultdict

def group_anagrams(words):
    groups = defaultdict(list)
    for word in words:
        key = "".join(sorted(word))  # "eat" -> "aet"
        groups[key].append(word)
    return list(groups.values())

print(group_anagrams(["eat", "tea", "tan", "ate", "nat", "bat"]))
# [['eat', 'tea', 'ate'], ['tan', 'nat'], ['bat']]
```

`defaultdict(list)` is a handy shortcut: if a key doesn't exist, it automatically creates an empty list instead of raising an error.

### Complexity in detail

**Two Sum**:
- Time: We walk through the array once, and each lookup/insert in the hashmap is O(1) on average. Total: **O(n)**.
- Space: In the worst case, we store all n numbers in the hashmap. **O(n)**.

**Why "on average" and not "always"?** In extremely rare bad cases, many keys might collide (map to the same address), and the hashmap slows down to O(n) per lookup. In practice, Python's dict handles this well, so we say O(1) average.

**Time-space tradeoff**: hashmaps use MORE space (O(n)) to save TIME (O(n) instead of O(n²)). This tradeoff is one of the most important ideas in programming!

### Common beginner mistakes
1. **Using a list as a dict key** — lists aren't hashable. Use tuples: `d[(1, 2)] = "value"`.
2. **Adding to a dict while iterating over it** — collect keys first, then modify.
3. **Using `dict[key]` when the key might not exist** — use `dict.get(key, default)` or `defaultdict`.

---

## 6. Intervals

### What is it?
An **interval** is a range with a start and end, like `[3, 7]` (meaning "from 3 to 7"). Interval problems ask about overlaps, merging, or scheduling.

### Real-world analogy
Think of **meeting times on a calendar**. Each meeting is an interval like `[9:00, 10:30]`. Questions like "do these two meetings conflict?", "what's the minimum number of rooms I need?", or "which meetings do I need to cancel?" are all interval problems.

### The golden rule: SORT FIRST
Almost every interval problem starts with sorting — usually by start time. Once sorted, you can process intervals from left to right and reason about them.

### Real-world scenario: merging vacation days

You're a manager, and your employees submitted vacation requests. Some overlap. You want to see the combined "office is understaffed" ranges.

```
Requests:  [1, 3], [2, 6], [8, 10], [15, 18]
```

After sorting by start (already sorted here), sweep left to right:
- Start with [1, 3].
- Next is [2, 6]. It overlaps [1, 3] (since 2 ≤ 3), so merge to [1, 6].
- Next is [8, 10]. 8 > 6, no overlap. Start a new interval.
- Next is [15, 18]. 15 > 10, no overlap. Start a new interval.

Result: `[[1, 6], [8, 10], [15, 18]]`.

### Walkthrough example: Merge overlapping intervals

```python
def merge(intervals):
    # Step 1: Sort by start time
    intervals.sort(key=lambda x: x[0])
    
    merged = []
    for start, end in intervals:
        # If merged is empty OR no overlap with last merged interval
        if not merged or start > merged[-1][1]:
            merged.append([start, end])
        else:
            # Overlap — extend the last interval's end
            merged[-1][1] = max(merged[-1][1], end)
    
    return merged
```

**Trace with `[[1, 3], [2, 6], [8, 10], [15, 18]]`**:

| Interval  | merged[-1] | Overlap? | Action              | merged after            |
|-----------|------------|----------|---------------------|-------------------------|
| [1, 3]    | none       | —        | append              | [[1, 3]]                |
| [2, 6]    | [1, 3]     | yes(2≤3) | extend end to 6     | [[1, 6]]                |
| [8, 10]   | [1, 6]     | no(8>6)  | append              | [[1, 6], [8, 10]]       |
| [15, 18]  | [8, 10]    | no(15>10)| append              | [[1, 6], [8, 10], [15, 18]] |

### Real-world scenario: minimum meeting rooms

You have 5 meetings. What's the fewest rooms you need?

**Idea**: sort by start time. Use a min-heap to track when the earliest-ending currently-active meeting frees up its room. For each new meeting:
- If the earliest-ending meeting has ended before this one starts, reuse that room (pop from heap).
- Push this meeting's end time onto the heap.
- Heap size = rooms currently in use.

```python
import heapq

def min_meeting_rooms(intervals):
    intervals.sort(key=lambda x: x[0])
    heap = []  # end times of active meetings
    for start, end in intervals:
        if heap and heap[0] <= start:
            heapq.heappop(heap)  # a room freed up
        heapq.heappush(heap, end)
    return len(heap)
```

### Complexity in detail

**Merge intervals**:
- **Time**: Sorting is O(n log n). Sweep is O(n). Total: **O(n log n)**. The sort dominates.
- **Space**: The output list can be up to n intervals. **O(n)**.

**Why is sorting always the bottleneck?** Because you can't do interval problems without knowing the order, and sorting is the fastest way to get order — O(n log n).

### Common beginner mistakes
1. **Forgetting to sort first** — most interval algorithms only work on sorted input.
2. **Getting overlap conditions wrong** — is `[1, 3]` and `[3, 5]` an overlap? Depends on the problem. Read carefully.
3. **Sorting by end time when you should sort by start time (or vice versa)** — different problems need different orderings.

---

## 7. Stack

### What is it?
A **stack** is a Last-In-First-Out (LIFO) collection. You add to the top and remove from the top.

### Real-world analogy
A **stack of plates** in a cafeteria. You put a new plate on top, and you take a plate from the top. You can't take a plate from the middle without removing everything above it.

Another analogy: the **undo button** in a text editor. Every action you take is pushed onto a stack. When you press undo, the last action is popped off.

### In Python
Just use a list! `append()` and `pop()` are both O(1) on a list.

```python
stack = []
stack.append(1)   # push
stack.append(2)
stack.append(3)   # stack is now [1, 2, 3]
top = stack.pop() # returns 3; stack is [1, 2]
```

### When to use it
- **Matching pairs**: parentheses, brackets, HTML tags
- **Reversing order**: last item comes out first
- **Tracking "context"**: nested function calls, folder navigation (Back button)
- **Monotonic stack**: keeping elements in sorted order (advanced)

### Real-world scenario: browser Back button

Every time you visit a new page, it gets pushed on a stack. When you press Back, the current page is popped, revealing the previous one.

### Walkthrough example: Valid parentheses

**Problem**: Is the string `"({[]})"` a valid combination of opening and closing brackets?

**Idea**: 
- When you see an opener like `(`, push it onto the stack.
- When you see a closer like `)`, pop the top of the stack. It must be the matching opener `(`. If not, invalid.
- At the end, the stack must be empty (all openers matched).

```python
def is_valid(s):
    stack = []
    pairs = {')': '(', ']': '[', '}': '{'}
    
    for char in s:
        if char in pairs:  # a closing bracket
            if not stack or stack.pop() != pairs[char]:
                return False
        else:  # an opening bracket
            stack.append(char)
    
    return not stack  # True if empty
```

**Trace with "({[]})"**:

| char | Action                          | Stack after     |
|------|---------------------------------|-----------------|
| '('  | push                            | ['(']           |
| '{'  | push                            | ['(', '{']      |
| '['  | push                            | ['(', '{', '['] |
| ']'  | pop '[' — matches ']'           | ['(', '{']      |
| '}'  | pop '{' — matches '}'           | ['(']           |
| ')'  | pop '(' — matches ')'           | []              |

Stack is empty at the end → valid!

### Complexity in detail

**Time**: We process each character once. Push and pop are O(1). Total: **O(n)**.

**Space**: The stack can grow up to n (imagine "(((((..."). **O(n)**.

### Common beginner mistakes
1. **Using `list.pop(0)`** — that removes from the FRONT, which is O(n)! Always use `list.pop()` (no argument = remove last).
2. **Trying to access `stack[-1]` when the stack is empty** — always check `if stack:` first.
3. **Forgetting to check emptiness at the end** — for parenthesis problems, unmatched openers left over = invalid.

---

## 8. Linked List

### What is it?
A **linked list** is a chain of nodes, where each node holds a value and a pointer to the next node.

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
```

### Real-world analogy
A **treasure hunt**. Each clue tells you where the next clue is. To find the 5th clue, you have to follow clues 1 → 2 → 3 → 4 → 5. There's no shortcut to jumping directly to clue 5.

Another analogy: a **train**. Each train car (node) is connected to the next by a coupling (the pointer). To reach the caboose, you walk through each car.

### Array vs Linked List

|                     | Array (list)             | Linked list               |
|---------------------|--------------------------|---------------------------|
| Access element      | O(1) — direct address    | O(n) — walk from start    |
| Insert at start     | O(n) — shift everything  | O(1) — just update head   |
| Insert at end       | O(1) if you have pointer | O(1) if you have tail ptr |
| Insert in middle    | O(n)                     | O(1) with pointer         |
| Memory              | Contiguous               | Scattered (each node)     |

### When to use a linked list
- You need frequent insertions and deletions in the middle
- You don't need random access (like `arr[42]`)
- The size changes a lot

### Key techniques

**1. The dummy head trick** — create a fake node before the head. This eliminates edge cases when the actual head changes.

**2. Fast/slow pointers** — one pointer moves twice as fast. Great for:
- Finding the middle of a list
- Detecting a cycle
- Finding the nth-from-end element

**3. Reversing** — the classic! Use three pointers: `prev`, `curr`, `next`.

### Walkthrough example: Reverse a linked list

**Problem**: Turn `1 → 2 → 3 → None` into `3 → 2 → 1 → None`.

**Idea**: walk through the list. For each node, make it point to the PREVIOUS node instead of the next one. We need to save the next node before we overwrite the pointer.

```python
def reverse_list(head):
    prev = None
    curr = head
    while curr:
        next_node = curr.next   # 1) Save what's next
        curr.next = prev        # 2) Reverse pointer
        prev = curr             # 3) Move prev forward
        curr = next_node        # 4) Move curr forward
    return prev
```

**Trace with `1 → 2 → 3`**:

| Step | prev | curr | next_node | Action                    | State after                |
|------|------|------|-----------|---------------------------|----------------------------|
| Init | None | 1    | —         | —                         | 1→2→3, prev=None           |
| 1    | None | 1    | 2         | 1.next = None             | 1→None; prev=1, curr=2     |
| 2    | 1    | 2    | 3         | 2.next = 1                | 2→1→None; prev=2, curr=3   |
| 3    | 2    | 3    | None      | 3.next = 2                | 3→2→1→None; prev=3         |
| End  | 3    | None | —         | loop exits                | return prev = 3            |

### Real-world scenario: detecting a cycle

Sometimes a linked list has a bug where a node points back to a previous node, creating a loop. How do you detect this without extra memory?

**Floyd's cycle detection (aka "tortoise and hare")**: two runners on a circular track. The fast one moves 2 steps per turn, the slow one moves 1. If there's a cycle, they'll eventually meet. If there's no cycle, fast reaches the end (None).

```python
def has_cycle(head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow is fast:
            return True
    return False
```

### Complexity in detail

**Reversal**:
- **Time**: We visit each node exactly once. **O(n)**.
- **Space**: We only use three pointers no matter how long the list is. **O(1)**.

**Cycle detection**:
- **Time**: If there's no cycle, we walk through in O(n). If there IS a cycle, the pointers meet within O(n) steps (mathematical fact). **O(n)**.
- **Space**: Just two pointers. **O(1)** — much better than a hashset of visited nodes!

### Common beginner mistakes
1. **Losing a reference before saving it**: `curr.next = prev` BEFORE `next_node = curr.next` — you've lost the rest of the list!
2. **Using `==` vs `is`** — for node identity, use `is` (they're the same object).
3. **Forgetting the null terminator** — the last node's `.next` must be `None`, or you have an infinite chain.

---

## 9. Binary Tree — DFS (Depth-First Search)

### What is it?
A **binary tree** is a tree structure where each node has up to two children (left and right). **DFS** means "go deep before going wide" — follow one path to the bottom before backtracking.

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
```

### Real-world analogy
An **exploration cave system**. You come to a fork in the tunnel. Rather than checking both, you go LEFT all the way down until you hit a dead end. Then you backtrack and try the next unexplored path.

Another analogy: a **family tree**. Grandpa has 2 kids, each kid has 2 kids, etc. DFS is like tracing one lineage down to the youngest descendant, then going back to check other branches.

### The three DFS orders

**Preorder (Root → Left → Right)**: process the node, then recurse into children.
Use when: you want to COPY the tree, or print it, top-down.

**Inorder (Left → Root → Right)**: recurse left, process the node, recurse right.
Use when: it's a Binary SEARCH Tree — gives you sorted output!

**Postorder (Left → Right → Root)**: recurse into children, then process the node.
Use when: you need info from BOTH children before deciding (like computing depth or deleting nodes).

### Real-world scenario: file system size

Given a folder structure (a tree!), calculate the total size of files.

Notice: to know a folder's total size, you must first know its subfolders' total sizes. This is a POSTORDER problem.

```python
def folder_size(node):
    if node is None:
        return 0
    left_size = folder_size(node.left)     # first, size of left subfolder
    right_size = folder_size(node.right)   # then, size of right subfolder
    return node.val + left_size + right_size  # finally, this folder's total
```

### Walkthrough example: Maximum depth of a tree

**Problem**: How deep is the tree? The tree
```
    3
   / \
  9   20
     /  \
    15   7
```
has depth 3 (path 3 → 20 → 15 or 3 → 20 → 7).

**Idea**: the depth of a tree is 1 + max(depth of left subtree, depth of right subtree).

```python
def max_depth(root):
    if root is None:
        return 0
    left_depth = max_depth(root.left)
    right_depth = max_depth(root.right)
    return 1 + max(left_depth, right_depth)
```

**Trace**:
- `max_depth(3)` calls `max_depth(9)` and `max_depth(20)`.
- `max_depth(9)` → 9 has no children → return 1.
- `max_depth(20)` calls `max_depth(15)` and `max_depth(7)`. Both return 1. So `max_depth(20)` returns 2.
- Back at `max_depth(3)`: `1 + max(1, 2) = 3`. ✅

### Understanding recursion (crucial for trees!)

Recursion is a function calling itself with a smaller version of the same problem. Two things you MUST have:
1. **Base case**: when to stop recursing (usually `if node is None: return`)
2. **Recursive step**: how to break the problem into smaller pieces

Beginners often struggle with "how does the computer keep track?" The answer: it uses a **call stack** — every recursive call is a plate on the stack. When a call returns, its plate is removed.

### Complexity in detail

**Time**: We visit each node exactly once. **O(n)** where n is the number of nodes.

**Space**: This is where it gets interesting.
- We use recursion, and the deepest call stack is the height of the tree.
- **Balanced tree** (like a well-shaped tree): height is log(n). Space is **O(log n)**.
- **Skewed tree** (like a linked list): height is n. Space is **O(n)**.

For a tree with 1,000,000 nodes:
- Balanced: recursion depth of about 20. Fine.
- Skewed: recursion depth of 1,000,000. **Python's default recursion limit is 1000!** You'd get a stack overflow. Use `sys.setrecursionlimit(10**6)` or convert to iterative.

### Common beginner mistakes
1. **Forgetting the base case** — infinite recursion → crash.
2. **Not returning from recursive calls** — the "info bubbling up" is lost.
3. **Confusing "what I return" vs "outer state I modify"** — pick one strategy and be consistent.

---

## 10. Binary Tree — BFS (Breadth-First Search)

### What is it?
**BFS** means "go wide before going deep". Visit all nodes at depth 1 before visiting any at depth 2. Uses a **queue** (First-In-First-Out).

### Real-world analogy
A **rumor spreading through a school**. On day 1, you tell 3 friends. On day 2, those 3 friends each tell 3 more. Everyone at distance 1 hears it before anyone at distance 2.

Another analogy: **ripples in a pond**. Drop a pebble; the ripple expands outward one layer at a time.

### DFS vs BFS

| Feature      | DFS                           | BFS                              |
|--------------|-------------------------------|----------------------------------|
| Data struct  | Stack (or recursion)          | Queue                            |
| Order        | Deep first, wide later        | Wide first, deep later           |
| Best for     | Path exists? All leaves?      | Shortest path, level-by-level    |
| Memory       | O(height)                     | O(width)                         |

### When to use BFS
- **Shortest path** in an unweighted graph
- **Level-by-level processing** ("print each level of the tree")
- **Nearest** anything ("closest exit")

### Python's `deque` — the queue you need

```python
from collections import deque
q = deque()
q.append(1)       # add to right
q.append(2)
q.append(3)       # deque: [1, 2, 3]
first = q.popleft()  # returns 1; deque: [2, 3]
```

Why not use a list? Because `list.pop(0)` is O(n) — Python has to shift everything. `deque.popleft()` is O(1).

### Walkthrough example: Level order traversal

**Problem**: Given the tree
```
    3
   / \
  9   20
     /  \
    15   7
```
Return `[[3], [9, 20], [15, 7]]` — each sublist is a level.

**Idea**: use a queue. At each step, capture the current queue size (= nodes on this level). Process exactly that many nodes, adding their children as you go. That gives you one level at a time.

```python
from collections import deque

def level_order(root):
    if not root:
        return []
    
    result = []
    q = deque([root])
    
    while q:
        level_size = len(q)   # freeze current level's size
        level = []
        for _ in range(level_size):
            node = q.popleft()
            level.append(node.val)
            if node.left:
                q.append(node.left)
            if node.right:
                q.append(node.right)
        result.append(level)
    
    return result
```

**Trace**:

| Iteration | Queue at start | level_size | After processing              | Level captured |
|-----------|----------------|------------|-------------------------------|----------------|
| 1         | [3]            | 1          | q = [9, 20]                   | [3]            |
| 2         | [9, 20]        | 2          | q = [15, 7]                   | [9, 20]        |
| 3         | [15, 7]        | 2          | q = []                        | [15, 7]        |

Result: `[[3], [9, 20], [15, 7]]`.

### Real-world scenario: shortest exit from a maze

You have a grid. Some cells are walls, others are paths. Find the shortest path from start to exit.

BFS is perfect: it explores all cells at distance 1, then all at distance 2, etc. The first time you reach the exit, you've found the shortest path — guaranteed.

### Complexity in detail

**Time**: We visit each node once. **O(n)**.

**Space**: The queue holds at most one full level of the tree. For a balanced tree, the widest level has n/2 nodes. So space is **O(n)** in the worst case (specifically, the number of nodes at the widest level).

### Common beginner mistakes
1. **Using `list.pop(0)` instead of `deque.popleft()`** — turns O(n) into O(n²)!
2. **Forgetting to freeze `len(q)` at the start of each level** — you'll process nodes from multiple levels mixed together.
3. **Adding None to the queue** — always check `if node.left:` before appending.

---

## 11. Binary Search Tree (BST)

### What is it?
A **BST** is a binary tree with a strict rule: for every node,
- All values in the LEFT subtree are LESS THAN the node's value.
- All values in the RIGHT subtree are GREATER THAN the node's value.

### Real-world analogy
Think of the **Dewey Decimal system** in a library, or the **way you look up a name in a printed dictionary**. If you're looking for "Michael" and open to "Peter", you know to look in the LEFT half. If you open to "Kevin", look in the RIGHT half.

### Why is this useful?
Search, insert, and delete are all O(log n) IF the tree is balanced. That's the same speed as binary search!

### The magic property: inorder traversal is SORTED

Because of the BST property, if you do an inorder traversal (Left → Root → Right), you get values in sorted order. This is a huge hint for many BST problems!

### Walkthrough example: Validate a BST

**Problem**: Given a binary tree, check if it's actually a valid BST.

**Common beginner mistake**: just checking `node.left.val < node.val < node.right.val` at each node. This is WRONG!

Why? Consider:
```
       5
      / \
     3   8
        / \
       4   9
```
At node 8, its left child 4 is less than 8 — passes the local check. But 4 is in the RIGHT subtree of 5, so 4 must be > 5. It isn't! This is not a valid BST.

**Correct idea**: pass down MIN and MAX bounds. Every value must be strictly between its inherited bounds.

```python
def is_valid_bst(root):
    def check(node, lo, hi):
        if node is None:
            return True
        if not (lo < node.val < hi):
            return False
        return (check(node.left, lo, node.val) and 
                check(node.right, node.val, hi))
    
    return check(root, float('-inf'), float('inf'))
```

The trick: when we recurse LEFT, we tighten the upper bound to the current value. When we recurse RIGHT, we tighten the lower bound.

### Real-world scenario: kth smallest element

Given a BST, find the 3rd smallest value.

Since inorder gives sorted order, just do an inorder traversal and count. Stop at the 3rd one.

```python
def kth_smallest(root, k):
    stack = []
    node = root
    while stack or node:
        # go as left as possible
        while node:
            stack.append(node)
            node = node.left
        node = stack.pop()
        k -= 1
        if k == 0:
            return node.val
        node = node.right
```

### Complexity in detail

**Balanced BST**: search, insert, delete are all **O(log n)**. Think of it like binary search — each step cuts the problem in half.

**Unbalanced BST** (worst case = linked-list-shaped): all operations degrade to **O(n)**. For interview problems, we usually assume reasonably balanced trees.

**Why log n?** If a tree is balanced, its height is about log₂(n). Each level of recursion cuts n in half:
- n = 1,000,000 → height about 20
- n = 1,000,000,000 → height about 30

That's why BSTs are so powerful: they scale beautifully.

### Common beginner mistakes
1. **The local-check-only mistake** for validation (shown above).
2. **Not handling duplicates** — is `[1, 1, 2]` a valid BST? Depends on the problem's rules.
3. **Assuming a random tree is a BST** — it may not be. Always check the problem statement.

---

## 12. Graph — DFS

### What is it?
A **graph** is a set of nodes connected by edges. Unlike a tree, a graph can have cycles, and a node can have any number of connections.

### Real-world analogy
- **Social network**: people are nodes, friendships are edges.
- **Road map**: cities are nodes, roads are edges.
- **Website**: pages are nodes, links are edges.

### Trees vs Graphs

| Feature | Tree                | Graph                      |
|---------|---------------------|----------------------------|
| Cycles  | No                  | Yes (usually)              |
| Root    | One                 | No special starting point  |
| Edges   | Exactly n-1         | Any number                 |

### How to represent a graph in Python

**Adjacency list** (most common): a dict where each key is a node and the value is a list of neighbors.

```python
graph = {
    'A': ['B', 'C'],
    'B': ['A', 'D'],
    'C': ['A', 'D'],
    'D': ['B', 'C']
}
# Edges: A-B, A-C, B-D, C-D
```

### The KEY challenge: avoid infinite loops!

Since graphs can have cycles, you need a **visited set**. Never re-visit a node.

### Walkthrough example: Number of islands

**Problem**: You have a 2D grid where '1' is land and '0' is water. An "island" is a connected group of '1's (connected horizontally or vertically). How many islands?

```
Input:
1 1 0 0 0
1 1 0 0 1
0 0 0 1 1
0 0 0 0 0

Output: 2
```

**Idea**: walk through every cell. When you find land, do a DFS to "sink" the entire island (mark it as water so you don't count it twice). Increment the island counter.

```python
def num_islands(grid):
    if not grid:
        return 0
    rows, cols = len(grid), len(grid[0])
    count = 0
    
    def dfs(r, c):
        # base case: out of bounds or not land
        if not (0 <= r < rows and 0 <= c < cols) or grid[r][c] != '1':
            return
        grid[r][c] = '0'  # sink this land
        # recurse in 4 directions
        dfs(r + 1, c)
        dfs(r - 1, c)
        dfs(r, c + 1)
        dfs(r, c - 1)
    
    for r in range(rows):
        for c in range(cols):
            if grid[r][c] == '1':
                count += 1
                dfs(r, c)  # sink the entire island
    
    return count
```

### Real-world scenario: friend groups on Facebook

You have a friendship graph. How many separate "friend groups" (connected components) exist? Same algorithm — DFS from each unvisited node counts as one group.

### Complexity in detail

**Number of islands**:
- **Time**: We visit each cell at most twice (once by the outer loop, once by DFS). If the grid is m × n, that's **O(m × n)**.
- **Space**: The DFS recursion stack can go as deep as m × n (in the worst case of one giant snake-shaped island). **O(m × n)**.

**In general for graph DFS**:
- **Time**: **O(V + E)** where V = nodes, E = edges. Each node and edge is examined once.
- **Space**: **O(V)** for the visited set + recursion stack.

### Common beginner mistakes
1. **Forgetting the visited set** — infinite loop on cyclic graphs!
2. **Marking as visited when returning instead of when entering** — leads to double-visits.
3. **Modifying the graph while iterating** — either use a copy or clearly plan the modifications.

---

## 13. Graph — BFS

### What is it?
Same as tree BFS: use a queue, process nodes level by level. On a graph, we ALSO need a visited set.

### Why BFS on graphs is special: SHORTEST PATH

**BFS on an unweighted graph gives you the shortest path.** This is a huge deal.

Why? Because BFS explores in "waves". The first time you reach a node, it's via the shortest possible route. Any other path would have to be longer (because BFS would've found it first if shorter).

### Real-world analogy
Imagine dropping a **droplet of dye in a swimming pool**. It spreads outward in concentric circles. The dye reaches nearby points first, farther points later. That's BFS.

### Walkthrough example: Shortest path in a maze

**Problem**: Given a grid, find the shortest number of steps from start (0, 0) to end (n-1, n-1). You can move up/down/left/right, and 0 = open, 1 = wall.

```python
from collections import deque

def shortest_path(grid):
    if not grid or grid[0][0] == 1:
        return -1
    n = len(grid)
    if grid[n-1][n-1] == 1:
        return -1
    
    q = deque([((0, 0), 1)])   # (position, distance)
    seen = {(0, 0)}
    
    while q:
        (r, c), d = q.popleft()
        if (r, c) == (n-1, n-1):
            return d
        for dr, dc in [(-1,0),(1,0),(0,-1),(0,1)]:
            nr, nc = r + dr, c + dc
            if 0 <= nr < n and 0 <= nc < n and grid[nr][nc] == 0 and (nr, nc) not in seen:
                seen.add((nr, nc))
                q.append(((nr, nc), d + 1))
    
    return -1
```

**Why does this find the SHORTEST path?** Because we process cells in order of distance. As soon as we reach the target, we know its distance is minimal.

### Real-world scenario: Six degrees of Kevin Bacon

Given an actor, find the shortest chain of "co-starred with" relationships to Kevin Bacon. BFS from the actor: layer 1 = direct co-stars, layer 2 = co-stars of co-stars, etc.

### Multi-source BFS

Sometimes you start from MULTIPLE places at once. Just add all starting positions to the queue at the beginning!

Example: rotting oranges. Some oranges are rotten (multiple sources). Every minute, adjacent fresh oranges become rotten. How many minutes until all oranges are rotten?

```python
def rotting_oranges(grid):
    rows, cols = len(grid), len(grid[0])
    q = deque()
    fresh = 0
    
    # Initialize: enqueue ALL rotten oranges as starting points
    for r in range(rows):
        for c in range(cols):
            if grid[r][c] == 2:
                q.append((r, c, 0))
            elif grid[r][c] == 1:
                fresh += 1
    
    max_time = 0
    while q:
        r, c, t = q.popleft()
        max_time = max(max_time, t)
        for dr, dc in [(-1,0),(1,0),(0,-1),(0,1)]:
            nr, nc = r + dr, c + dc
            if 0 <= nr < rows and 0 <= nc < cols and grid[nr][nc] == 1:
                grid[nr][nc] = 2
                fresh -= 1
                q.append((nr, nc, t + 1))
    
    return max_time if fresh == 0 else -1
```

### Complexity in detail

**Grid BFS**: **O(m × n)** time and space (same reasoning as DFS).

**General graph BFS**: **O(V + E)** time, **O(V)** space.

### Common beginner mistakes
1. **Marking visited when POPPING from queue, not when PUSHING** — you'll add the same node to the queue many times, blowing up memory.
2. **Using DFS when the problem needs shortest path** — DFS gives A path, not the SHORTEST path.
3. **Not tracking distance** — either add it as part of the queue element, or process one level at a time.

---

## 14. Trie (Prefix Tree)

### What is it?
A **trie** is a tree specifically for storing strings, where each edge represents one character. It's designed for lightning-fast prefix lookups.

### Real-world analogy
Think of the **autocomplete feature on your phone**. As you type "ap", it instantly shows "apple", "app", "appointment". How? It walks down a trie: A → P → and then finds all words in that subtree.

Another analogy: a **branching decision tree**. To spell "cat", you go C → A → T. To spell "car", you go C → A → R. C-A is shared between them.

### Structure

```
        (root)
        /    \
       c      d
       |      |
       a      o
      / \     |
     t   r    g
```
This trie contains: "cat", "car", "dog".

### When to use a trie
- **Autocomplete / prefix search**: "find all words starting with 'app'"
- **Spell check**
- **IP routing**: longest prefix match on IP addresses
- **Word puzzles**: word search, Boggle

### Walkthrough example: Implementing a Trie

```python
class Trie:
    def __init__(self):
        self.children = {}    # char -> Trie node
        self.is_word = False  # marks end of a complete word
    
    def insert(self, word):
        node = self
        for char in word:
            if char not in node.children:
                node.children[char] = Trie()
            node = node.children[char]
        node.is_word = True
    
    def search(self, word):
        node = self._find(word)
        return node is not None and node.is_word
    
    def starts_with(self, prefix):
        return self._find(prefix) is not None
    
    def _find(self, s):
        node = self
        for char in s:
            if char not in node.children:
                return None
            node = node.children[char]
        return node
```

**Usage**:
```python
trie = Trie()
trie.insert("apple")
trie.insert("app")

trie.search("apple")       # True
trie.search("app")         # True
trie.search("appl")        # False (not a full word)
trie.starts_with("appl")   # True
```

### Complexity in detail

**Insert / search / prefix**: **O(L)** where L is the length of the word.

Why is this cool? Because it's independent of how many words are in the trie! A trie with 1 million words takes just as long to search for "hello" as a trie with 10 words. That's because we walk down at most L characters.

**Space**: O(total characters across all words). Can be big, but each character is shared with other words that have the same prefix.

### Common beginner mistakes
1. **Forgetting the `is_word` flag** — can't distinguish "app" (a word) from "app" (a prefix of "apple").
2. **Using a fixed array `[None] * 26`** when you should use a dict — only works for lowercase English.
3. **Copying the wrong node** — always be clear whether you're at the root or at a child.

---

## 15. Backtracking

### What is it?
**Backtracking** is a systematic way to try all possibilities. It builds solutions step by step, and abandons ("backtracks") when the current path can't lead to a valid answer.

### Real-world analogy
Solving a **maze with a piece of chalk**. You mark your path as you go. When you hit a dead end, you erase your marks going back to the last fork and try a different direction.

Another analogy: **filling out a Sudoku puzzle**. You try a number. If it leads to a contradiction, you erase it and try another. Systematic trial and error.

### The template
Every backtracking solution has three parts:
1. **Choose**: make a decision (add to current path)
2. **Explore**: recurse to try more decisions
3. **Un-choose**: undo the decision (remove from path) to try alternatives

```python
def backtrack(path, choices):
    if is_solution(path):
        results.append(path[:])   # save a COPY
        return
    for choice in choices:
        if is_valid(choice, path):
            path.append(choice)   # 1. choose
            backtrack(path, ...)  # 2. explore
            path.pop()            # 3. un-choose
```

### Walkthrough example: All subsets

**Problem**: Given `[1, 2, 3]`, return all subsets:
```
[], [1], [2], [3], [1,2], [1,3], [2,3], [1,2,3]
```

**Idea**: at each step, decide whether to include the current element or not.

```python
def subsets(nums):
    result = []
    path = []
    
    def backtrack(start):
        result.append(path[:])  # every state is a valid subset
        for i in range(start, len(nums)):
            path.append(nums[i])       # choose
            backtrack(i + 1)           # explore (i+1: don't reuse)
            path.pop()                 # un-choose
    
    backtrack(0)
    return result
```

**Trace with `[1, 2, 3]`** (partial):
```
backtrack(0)  path=[]      → save []
  choose 1, path=[1]
  backtrack(1)              → save [1]
    choose 2, path=[1,2]
    backtrack(2)            → save [1,2]
      choose 3, path=[1,2,3]
      backtrack(3)          → save [1,2,3]
      unchoose 3, path=[1,2]
    unchoose 2, path=[1]
    choose 3, path=[1,3]
    backtrack(3)            → save [1,3]
    unchoose 3, path=[1]
  unchoose 1, path=[]
  ...
```

### Real-world scenario: scheduling conflicts

You have 5 tasks with time constraints. Some tasks depend on others. Find all valid schedules. Backtracking tries all orderings, pruning invalid ones (like violating dependencies).

### Complexity in detail

Backtracking is usually **exponential** — for n items, up to O(2ⁿ) subsets or O(n!) permutations.

- **Subsets**: 2ⁿ subsets, each up to length n. Total: **O(n × 2ⁿ)**.
- **Permutations**: n! permutations. Total: **O(n × n!)**.

This sounds terrible, but for n ≤ 20 or so, it's feasible. And it's often the ONLY way to solve certain problems (like N-Queens).

**Pruning is key**: cutting off bad branches early massively reduces the actual runtime.

### Common beginner mistakes
1. **Appending `path` instead of `path[:]`** — you're storing the same list reference, and it keeps changing!
2. **Forgetting to un-choose** — corrupts other branches.
3. **Not thinking about pruning** — some problems become impossible without it.

---

## 16. Divide and Conquer

### What is it?
Break a problem into smaller subproblems, solve them independently, then combine the results.

### Real-world analogy
**Sorting a huge deck of playing cards** with a friend. Split the deck in half. Each of you sorts your half. Then merge the two sorted halves. That's merge sort!

Or think of a **corporate hierarchy** solving a company-wide problem. The CEO splits it among VPs, who split it among directors, who split it among managers. Each solves their piece, and the results roll back up.

### The recipe
1. **Divide**: split the problem into smaller pieces
2. **Conquer**: solve each piece (usually recursively)
3. **Combine**: merge the results

### Walkthrough example: Merge sort

**Problem**: sort `[38, 27, 43, 3, 9, 82, 10]`.

**Idea**:
1. Split into two halves.
2. Recursively sort each half.
3. Merge the two sorted halves.

```python
def merge_sort(arr):
    if len(arr) <= 1:
        return arr
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
    return merge(left, right)

def merge(a, b):
    result = []
    i = j = 0
    while i < len(a) and j < len(b):
        if a[i] <= b[j]:
            result.append(a[i])
            i += 1
        else:
            result.append(b[j])
            j += 1
    result.extend(a[i:])
    result.extend(b[j:])
    return result
```

**Trace** (simplified):
```
[38, 27, 43, 3, 9, 82, 10]
     /                 \
[38, 27, 43]      [3, 9, 82, 10]
   / \                /       \
[38] [27, 43]     [3, 9]   [82, 10]
        / \       / \        / \
      [27][43]  [3][9]     [82][10]
        \ /       \ /        \ /
       [27, 43]  [3, 9]    [10, 82]
   \    /            \     /
[27, 38, 43]        [3, 9, 10, 82]
        \             /
   [3, 9, 10, 27, 38, 43, 82]
```

### Complexity in detail

**Merge sort**:
- **Time**: **O(n log n)**. Here's why:
  - Each level of recursion has n total elements to merge.
  - The depth of the recursion is log n (halving each time).
  - Total work: n × log n.
- **Space**: **O(n)** for the temporary arrays during merging.

**The Master Theorem** (advanced): for `T(n) = a × T(n/b) + f(n)`, complexity depends on how `f(n)` compares to `n^(log_b a)`. For merge sort: a = 2, b = 2, f(n) = n. Formula gives O(n log n).

### Common beginner mistakes
1. **Recomputing base case each time** — always specify the smallest problem you can solve directly.
2. **Forgetting to actually COMBINE the results** — the "merge" step is where the magic happens.

---

## 17. Kadane's Algorithm

### What is it?
A brilliant O(n) algorithm to find the **maximum sum of any contiguous subarray**.

### Real-world analogy
Imagine you're **hiking a trail with ups and downs**. At each point, you can start your journey or continue from the previous point. Kadane's algorithm asks: should I keep going (add to my current streak) or start fresh from here?

The rule: if my previous streak has a NEGATIVE total, drop it — starting fresh is better.

### Walkthrough example

**Problem**: Given `[-2, 1, -3, 4, -1, 2, 1, -5, 4]`, find the max subarray sum.
Answer: `4 + (-1) + 2 + 1 = 6`.

```python
def max_subarray(nums):
    current = best = nums[0]
    for num in nums[1:]:
        current = max(num, current + num)
        best = max(best, current)
    return best
```

**The magic line**: `current = max(num, current + num)`. This asks: "Is extending my previous subarray better than starting fresh at this element?"

**Trace**:

| num | current + num | max(num, current+num) | current | best |
|-----|---------------|-----------------------|---------|------|
| -2  | —             | —                     | -2      | -2   |
| 1   | -1            | max(1, -1) = 1        | 1       | 1    |
| -3  | -2            | max(-3, -2) = -2      | -2      | 1    |
| 4   | 2             | max(4, 2) = 4         | 4       | 4    |
| -1  | 3             | max(-1, 3) = 3        | 3       | 4    |
| 2   | 5             | max(2, 5) = 5         | 5       | 5    |
| 1   | 6             | max(1, 6) = 6         | 6       | 6    |
| -5  | 1             | max(-5, 1) = 1        | 1       | 6    |
| 4   | 5             | max(4, 5) = 5         | 5       | 6    |

Answer: 6. ✅

### Real-world scenario: best stock streak

You have daily profit/loss values for a stock. What's the biggest cumulative gain if you had to hold the stock for consecutive days? Kadane's tells you.

### Complexity in detail

- **Time**: One pass through the array. **O(n)**.
- **Space**: Two variables. **O(1)**.

The naive approach checks every possible subarray: O(n³) or O(n²). Kadane's is a huge improvement.

### Common beginner mistakes
1. **Initializing `best = 0`** — wrong if all numbers are negative! Use `best = nums[0]`.
2. **Confusing subarray (contiguous) with subsequence (any order)** — different problem, different algorithm.

---

## 18. Binary Search

### What is it?
An algorithm to find something in a sorted array in O(log n). Instead of checking each element, you keep halving the search space.

### Real-world analogy
The **phonebook example** from the intro. Also: guessing a number between 1 and 100. Instead of guessing 1, 2, 3, ..., guess 50 (too high or too low?), then 25 or 75, and so on. You'll find it in at most 7 guesses.

### The core idea
Given a sorted array, use two pointers `lo` and `hi`. Look at the middle.
- If it's the target → done.
- If target is smaller → search the LEFT half.
- If target is bigger → search the RIGHT half.

### Walkthrough example

**Problem**: In `[1, 3, 5, 7, 9, 11, 13, 15]`, find 7.

```python
def binary_search(nums, target):
    lo, hi = 0, len(nums) - 1
    while lo <= hi:
        mid = (lo + hi) // 2
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            lo = mid + 1
        else:
            hi = mid - 1
    return -1
```

**Trace**:

| Step | lo | hi | mid | nums[mid] | Action                |
|------|----|----|-----|-----------|-----------------------|
| 1    | 0  | 7  | 3   | 7         | Found! Return 3.      |

Found in 1 step! For n = 8, at most 3 steps (log₂ 8 = 3). For n = 1,000,000, at most 20 steps.

### The two templates

Beginners often get confused between two variants:

**Template A: exact match**
```python
lo, hi = 0, len(nums) - 1
while lo <= hi:            # <=
    mid = (lo + hi) // 2
    if nums[mid] == target: return mid
    elif nums[mid] < target: lo = mid + 1
    else: hi = mid - 1
return -1
```

**Template B: leftmost insertion point** (finds where to insert to keep sorted)
```python
lo, hi = 0, len(nums)      # len(nums), not len(nums) - 1
while lo < hi:             # <, not <=
    mid = (lo + hi) // 2
    if nums[mid] < target: lo = mid + 1
    else: hi = mid         # not mid - 1
return lo
```

Pick one and internalize it! Python has this built in: `bisect.bisect_left(nums, target)`.

### Real-world scenario: binary search on the answer

**Problem**: You have to ship packages within D days. What's the minimum capacity ship you need?

**Idea**: 
- If capacity C works (D days is enough), then any bigger capacity also works.
- If C doesn't work, any smaller doesn't either.
- This is a monotonic property! Binary-search the capacity.

```python
def min_capacity(weights, days):
    def can_ship(cap):
        d, load = 1, 0
        for w in weights:
            if load + w > cap:
                d += 1
                load = 0
            load += w
        return d <= days
    
    lo, hi = max(weights), sum(weights)
    while lo < hi:
        mid = (lo + hi) // 2
        if can_ship(mid):
            hi = mid
        else:
            lo = mid + 1
    return lo
```

We're binary searching over the ANSWER VALUE (capacity), not an array index. This is a powerful pattern.

### Complexity in detail

- **Time**: Each step halves the search space. **O(log n)**.
- **Space**: **O(1)**.

**How dramatically log n grows** (or doesn't):

| n              | log₂ n |
|----------------|--------|
| 10             | ~3     |
| 1,000          | ~10    |
| 1,000,000      | ~20    |
| 1,000,000,000  | ~30    |

Binary search is why searching Google works even with trillions of pages.

### Common beginner mistakes
1. **Infinite loop from wrong pointer update** — mixing templates.
2. **Not checking that the array is sorted** — binary search only works on sorted data.
3. **Off-by-one on `lo` and `hi`** — trace through small examples to verify.

---

## 19. Heap (Priority Queue)

### What is it?
A **heap** (or **priority queue**) is a data structure that always gives you the smallest (or largest) element quickly.

### Real-world analogy
An **emergency room triage**. Patients aren't seen in the order they arrive — they're seen based on how urgent their condition is. The most critical case is always at the top of the priority list.

Another analogy: your **email inbox with "important" flag**. Important emails always show at the top, no matter when they arrived.

### How is it different from a sorted list?
- Sorted list: sorted at all times. Insert is O(n).
- Heap: only guarantees the smallest is on top. Insert is O(log n). Much faster.

### Python's `heapq`

Python's `heapq` is a **MIN-heap** (smallest on top). For a max-heap, negate the values.

```python
import heapq

heap = []
heapq.heappush(heap, 3)
heapq.heappush(heap, 1)
heapq.heappush(heap, 2)

heap[0]              # 1 (smallest)
heapq.heappop(heap)  # returns 1
heapq.heappop(heap)  # returns 2
```

### When to use a heap
- **Top-K problems**: "the 5 largest numbers", "the 10 most common words"
- **Merging K sorted lists**
- **Scheduling** by priority
- **Median from a data stream** (two heaps trick)
- **Dijkstra's shortest path**

### Walkthrough example: Kth largest element

**Problem**: In `[3, 2, 1, 5, 6, 4]`, find the 2nd largest. Answer: 5.

**Idea**: keep a MIN-heap of size k. As you go through the list, push each number. If the heap exceeds size k, pop the smallest. At the end, the top of the heap is the kth largest.

Why? The heap always contains the k largest numbers seen so far. The smallest of those (heap top) is the kth largest.

```python
import heapq

def find_kth_largest(nums, k):
    heap = []
    for num in nums:
        heapq.heappush(heap, num)
        if len(heap) > k:
            heapq.heappop(heap)
    return heap[0]
```

**Trace with `[3, 2, 1, 5, 6, 4]`, k = 2**:

| num | heap after push | Size > 2? | heap after pop |
|-----|-----------------|-----------|----------------|
| 3   | [3]             | no        | [3]            |
| 2   | [2, 3]          | no        | [2, 3]         |
| 1   | [1, 3, 2]       | yes       | [2, 3]         |
| 5   | [2, 3, 5]       | yes       | [3, 5]         |
| 6   | [3, 5, 6]       | yes       | [5, 6]         |
| 4   | [4, 6, 5]       | yes       | [5, 6]         |

heap[0] = 5 ✅

### Real-world scenario: task scheduling

You have 100 tasks with priorities. Every minute, execute the highest-priority task. As new tasks arrive, they're added to the queue with their priorities. A heap handles this naturally:

```python
import heapq

tasks = []
heapq.heappush(tasks, (1, "critical bug fix"))   # priority 1 = highest
heapq.heappush(tasks, (3, "refactor CSS"))
heapq.heappush(tasks, (2, "deploy staging"))

while tasks:
    priority, task = heapq.heappop(tasks)
    print(f"Doing: {task}")
```

### Complexity in detail

- **Push / pop**: **O(log n)** — a heap is a tree with height log n. Bubbling up/down takes at most log n swaps.
- **Peek (top)**: **O(1)**.
- **Building a heap from a list (heapify)**: **O(n)**! Surprisingly fast.

**Comparison to alternatives**:
- Sorted list: insert = O(n), find min = O(1).
- Heap: insert = O(log n), find min = O(1).

For Top-K problem:
- Sorting entire list: O(n log n).
- Heap of size k: O(n log k). Much better when k << n.

### Common beginner mistakes
1. **Forgetting Python's heapq is a MIN-heap** — negate values for max-heap.
2. **Comparing non-comparable items** — for tuples, all elements must be comparable.
3. **Using `min(list)` in a loop** — that's O(n) per call. Use a heap for O(log n).

---

## 20. Bit Manipulation

### What is it?
Working with numbers at the **binary bit level** using operators like AND, OR, XOR, and bit shifts. Extremely fast.

### Real-world analogy
Think of a **row of light switches**. Each switch is on (1) or off (0). Bit operations let you flip, check, or combine switch states in bulk.

### Binary refresher
Every integer is stored in binary. `5` is `101` (4 + 0 + 1). `13` is `1101` (8 + 4 + 0 + 1).

### The operators

| Op   | Name  | Example              | What it does                          |
|------|-------|----------------------|---------------------------------------|
| `&`  | AND   | `6 & 3 = 2`          | 1 in both → 1                         |
| `|`  | OR    | `6 | 3 = 7`          | 1 in either → 1                       |
| `^`  | XOR   | `6 ^ 3 = 5`          | 1 in exactly one → 1                  |
| `~`  | NOT   | `~5 = -6`            | flip every bit                        |
| `<<` | LSHIFT| `1 << 3 = 8`         | multiply by 2^n                       |
| `>>` | RSHIFT| `8 >> 1 = 4`         | integer divide by 2^n                 |

### The most useful XOR identity

`x ^ x = 0` and `x ^ 0 = x`.

**Consequence**: if you XOR every number in a list where each appears TWICE except one, the pairs cancel and you're left with the unique one!

### Walkthrough example: Find the unique number

**Problem**: `[2, 3, 5, 3, 2]` — every number appears twice except 5. Find it.

```python
def single_number(nums):
    result = 0
    for num in nums:
        result ^= num
    return result
```

**Trace**:
- `0 ^ 2 = 2`
- `2 ^ 3 = 1` (binary: 10 ^ 11 = 01)
- `1 ^ 5 = 4` (binary: 001 ^ 101 = 100)
- `4 ^ 3 = 7` (binary: 100 ^ 011 = 111)
- `7 ^ 2 = 5` (binary: 111 ^ 010 = 101) ✅

The pairs cancel, leaving 5. No extra memory needed!

### Real-world scenario: permissions system

In Unix, file permissions use bits: read = 4 (100), write = 2 (010), execute = 1 (001).
- `chmod 7` = 4 + 2 + 1 = all permissions (`111`)
- To check "can write?": `permissions & 2` — nonzero means yes.
- To grant write: `permissions | 2`.
- To revoke write: `permissions & ~2`.

### Handy tricks
- **Check if a number is a power of 2**: `x > 0 and (x & (x - 1)) == 0`
- **Count 1-bits**: repeatedly do `x &= x - 1` (clears the lowest 1-bit)
- **Test bit i**: `x & (1 << i)`
- **Set bit i**: `x | (1 << i)`
- **Clear bit i**: `x & ~(1 << i)`

### Complexity in detail

Bitwise operations are **O(1)** on fixed-size integers (32 or 64 bits). Python integers are arbitrary precision, so bitwise on huge numbers is O(bits), but for typical problems it's effectively O(1).

### Common beginner mistakes
1. **Operator precedence**: `x & 1 == 0` doesn't do what you think! Use `(x & 1) == 0`.
2. **Signed vs unsigned confusion**: Python has no unsigned. `~x = -x - 1` in Python.
3. **Forgetting XOR is commutative and associative**: order doesn't matter.

---

## 21. Math

### What is it?
A grab-bag of number-related techniques: primes, GCD, powers, modular arithmetic.

### The big ones

**GCD (Greatest Common Divisor)** — Euclidean algorithm:
```python
from math import gcd
gcd(12, 18)   # 6

# By hand:
def my_gcd(a, b):
    while b:
        a, b = b, a % b
    return a
```

Why it works: `gcd(a, b) = gcd(b, a mod b)`. Ancient Greek elegance!

**Fast exponentiation** — compute `x^n` in O(log n):
```python
def power(x, n):
    result = 1
    while n > 0:
        if n & 1:            # if n is odd
            result *= x
        x *= x               # square x
        n >>= 1              # halve n
    return result
```

**Prime check**:
```python
def is_prime(n):
    if n < 2: return False
    if n < 4: return True
    if n % 2 == 0: return False
    i = 3
    while i * i <= n:
        if n % i == 0: return False
        i += 2
    return True
```

Only check up to √n because if n = a × b, at least one of a, b is ≤ √n.

### Real-world scenario: cryptography

Modern encryption (RSA) relies on:
- Fast exponentiation with modular arithmetic (`pow(base, exp, mod)` in Python)
- Prime numbers
- GCD

These aren't just interview trivia — they're the foundation of internet security!

### Complexity notes
- GCD: **O(log(min(a, b)))**
- Prime check: **O(√n)**
- Fast exponentiation: **O(log n)**
- Sum 1..n = `n*(n+1)//2`: **O(1)**

### Common beginner mistakes
1. **Using `/` when you mean `//`** — `/` gives float in Python 3.
2. **Integer overflow** — Python doesn't overflow (arbitrary precision), but be careful in other languages.
3. **Modular arithmetic mistakes** — remember `(a + b) % m == ((a % m) + (b % m)) % m`.

---

## 22. 1D Dynamic Programming

### What is it?
**Dynamic Programming (DP)** is solving a problem by combining solutions to smaller subproblems, and **remembering** the answers to avoid recomputing.

### Real-world analogy

**Climbing stairs**. There are 5 steps. You can go up 1 or 2 steps at a time. How many ways to reach the top?

If you know how many ways to reach step 4 (call it `w4`) and step 3 (call it `w3`), then ways to reach step 5 = w4 + w3 (last move was 1 or 2 steps). This is the Fibonacci pattern!

Another analogy: **making change**. If I know the fewest coins to make $0.05, $0.10, $0.15, etc., I can find the fewest for $1.00 by looking at solutions for $0.90 (add a dime), $0.75 (add a quarter), etc.

### Two styles

**Top-down (memoization)**: recurse, but cache the results.
```python
from functools import cache

@cache
def climb(n):
    if n <= 2:
        return n
    return climb(n - 1) + climb(n - 2)
```

**Bottom-up (tabulation)**: build up from small subproblems using a loop.
```python
def climb(n):
    if n <= 2:
        return n
    dp = [0] * (n + 1)
    dp[1], dp[2] = 1, 2
    for i in range(3, n + 1):
        dp[i] = dp[i - 1] + dp[i - 2]
    return dp[n]
```

Both give the same answer. Choose based on which is easier to think about.

### The DP recipe (for beginners)

1. **Define state**: what does `dp[i]` mean in plain English?
2. **Recurrence**: how does `dp[i]` relate to earlier states?
3. **Base case**: what are the smallest inputs?
4. **Iteration order**: which direction to fill?
5. **Answer**: which cell has the final answer?

### Walkthrough example: House Robber

**Problem**: A row of houses with money `[2, 7, 9, 3, 1]`. You can't rob two adjacent houses. Max money?

**State**: `dp[i]` = max money you can rob from houses 0..i.

**Recurrence**: at house i, you either:
- Skip it: `dp[i - 1]`
- Rob it: `dp[i - 2] + nums[i]` (can't rob i-1)

So `dp[i] = max(dp[i - 1], dp[i - 2] + nums[i])`.

```python
def rob(nums):
    if not nums: return 0
    if len(nums) == 1: return nums[0]
    
    dp = [0] * len(nums)
    dp[0] = nums[0]
    dp[1] = max(nums[0], nums[1])
    
    for i in range(2, len(nums)):
        dp[i] = max(dp[i - 1], dp[i - 2] + nums[i])
    
    return dp[-1]
```

**Trace with `[2, 7, 9, 3, 1]`**:

| i | nums[i] | dp[i-1] | dp[i-2] + nums[i] | dp[i]              |
|---|---------|---------|--------------------|--------------------|
| 0 | 2       | —       | —                  | 2                  |
| 1 | 7       | 2       | 7                  | max(2, 7) = 7      |
| 2 | 9       | 7       | 2 + 9 = 11         | max(7, 11) = 11    |
| 3 | 3       | 11      | 7 + 3 = 10         | max(11, 10) = 11   |
| 4 | 1       | 11      | 11 + 1 = 12        | max(11, 12) = 12   |

Answer: 12 (rob houses 0, 2, 4: $2 + $9 + $1 = $12).

### Space optimization
For many 1D DPs, we only need the last 2 values. Compress the array to constants:

```python
def rob(nums):
    prev2, prev1 = 0, 0
    for num in nums:
        prev2, prev1 = prev1, max(prev1, prev2 + num)
    return prev1
```

Space goes from O(n) to O(1)!

### Complexity in detail

**Time**: Each state is computed once. If there are n states and each takes O(1) time, total is **O(n)**.

**Space**: **O(n)** for the DP array, or **O(1)** if you optimize.

**Why is this fast?** Naive recursion (without memoization) is O(2ⁿ) — exponential! DP with memoization is O(n). For n = 40, that's 10¹² vs 40 operations. Huge win.

### Common beginner mistakes
1. **Wrong state definition** — spend time on step 1 of the recipe. Get it right and everything follows.
2. **Missing base case** — the whole table becomes garbage.
3. **Wrong iteration order** — some problems need to iterate backward.

---

## 23. Multi-D Dynamic Programming

### What is it?
DP where the state has **2 or more dimensions**, so it's a 2D table.

### When to use it
- **Grid DP**: dp[r][c] depends on dp[r-1][c] and dp[r][c-1]
- **Two-string DP**: dp[i][j] compares prefixes of two strings
- **Knapsack**: dp[i][w] = using first i items with capacity w
- **Interval DP**: dp[i][j] considers subrange from i to j

### Real-world analogy

**Comparing two documents for differences** (like `git diff`). The "edit distance" DP asks: what's the minimum number of edits (insertions, deletions, substitutions) to turn one string into another?

Or **finding common features in two products' feature lists** — the Longest Common Subsequence.

### Walkthrough example: Unique Paths in a Grid

**Problem**: In an m × n grid, start at top-left, reach bottom-right. Can only move right or down. How many paths?

**State**: `dp[r][c]` = number of ways to reach cell (r, c).

**Recurrence**: `dp[r][c] = dp[r-1][c] + dp[r][c-1]` (came from above or from left).

**Base**: `dp[0][0] = 1`. First row and column are all 1s.

```python
def unique_paths(m, n):
    dp = [[1] * n for _ in range(m)]
    for r in range(1, m):
        for c in range(1, n):
            dp[r][c] = dp[r - 1][c] + dp[r][c - 1]
    return dp[m - 1][n - 1]
```

**Trace for m=3, n=3**:
```
1 1 1
1 2 3
1 3 6
```
Answer: 6.

### Walkthrough example: Longest Common Subsequence

**Problem**: What's the longest sequence of characters that appears in both "abcde" and "ace" in the same order? Answer: "ace", length 3.

**State**: `dp[i][j]` = length of LCS between first i chars of A and first j chars of B.

**Recurrence**:
- If `A[i-1] == B[j-1]`: `dp[i][j] = dp[i-1][j-1] + 1`
- Else: `dp[i][j] = max(dp[i-1][j], dp[i][j-1])`

```python
def lcs(a, b):
    m, n = len(a), len(b)
    dp = [[0] * (n + 1) for _ in range(m + 1)]
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if a[i - 1] == b[j - 1]:
                dp[i][j] = dp[i - 1][j - 1] + 1
            else:
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1])
    return dp[m][n]
```

### Real-world scenario: spell checker

You type "recieve". The checker computes edit distance to every word in the dictionary. "receive" has edit distance 2 (swap two letters). It suggests the closest match.

### Complexity in detail

**Time**: We fill an m × n grid, each cell in O(1). Total: **O(m × n)**.

**Space**: **O(m × n)** for the table. Often can be reduced to O(min(m, n)) with clever tricks.

**Why does DP work here?** Brute force (try all subsequences of A and check in B) is exponential. DP is polynomial. For strings of length 1000, that's 10³⁰⁰ vs 10⁶. Not even the same universe.

### Common beginner mistakes
1. **Confusing i and j** — always name variables carefully.
2. **Off-by-one on the DP grid** — most 2D DPs use an extra row/column of zeros for the base case.
3. **Wrong dependency direction** — trace one small example before coding.

---

## Python Cheatsheet for Beginners

### Big O Cheat Sheet — Common Python Operations

| Operation                | Complexity     |
|--------------------------|----------------|
| `list[i]`                | O(1)           |
| `list.append(x)`         | O(1) amortized |
| `list.pop()`             | O(1)           |
| `list.pop(0)`            | O(n) ⚠️        |
| `list.insert(0, x)`      | O(n) ⚠️        |
| `x in list`              | O(n) ⚠️        |
| `x in set` or `dict`     | O(1) avg       |
| `dict[k] = v`            | O(1) avg       |
| `deque.appendleft(x)`    | O(1)           |
| `deque.popleft()`        | O(1)           |
| `heapq.heappush(h, x)`   | O(log n)       |
| `heapq.heappop(h)`       | O(log n)       |
| `sorted(list)`           | O(n log n)     |
| `str + str`              | O(n)           |
| `"".join(list)`          | O(n)           |

### Essential imports for interview problems
```python
from collections import Counter, defaultdict, deque, OrderedDict
from functools import cache, lru_cache, reduce
from itertools import combinations, permutations, product, accumulate
import heapq
import bisect
import math
import sys
```

### Handy patterns

```python
# Iterate with index
for i, x in enumerate(arr):
    ...

# Iterate two lists together
for a, b in zip(arr1, arr2):
    ...

# Reverse iteration
for x in reversed(arr):
    ...

# Sort with custom key
sorted(arr, key=lambda x: (x[0], -x[1]))

# Character counter
from collections import Counter
c = Counter("banana")  # {'a': 3, 'n': 2, 'b': 1}

# Default dict
from collections import defaultdict
d = defaultdict(list)
d[key].append(value)   # no KeyError

# Deque for BFS
from collections import deque
q = deque([start])

# Recursion limit for deep trees
import sys
sys.setrecursionlimit(10**6)

# Infinity for min/max initialization
float('inf'), float('-inf')

# Binary search
import bisect
bisect.bisect_left(sorted_arr, x)

# Memoization
from functools import cache
@cache
def solve(state):
    ...
```

### How much time is my algorithm allowed?

For a typical interview time limit (a few seconds), here's what's feasible:

| n up to    | Fastest allowed complexity |
|------------|----------------------------|
| 10⁸        | O(n)                       |
| 10⁶        | O(n log n)                 |
| 10⁴        | O(n²)                      |
| 500        | O(n³)                      |
| 25         | O(2ⁿ)                      |
| 12         | O(n!)                      |

This tells you what technique to reach for. n = 10⁵ and a nested loop won't fly.

---

## Study Plan (6 Weeks)

### Week 1: Foundations
- Array / String
- Two Pointers
- Sliding Window
- Hashmap

### Week 2: Linear structures
- Stack
- Linked List
- Intervals
- Matrix

### Week 3: Trees
- Binary Tree DFS
- Binary Tree BFS
- Binary Search Tree
- Trie

### Week 4: Search
- Binary Search
- Heap
- Backtracking

### Week 5: Graphs
- Graph DFS
- Graph BFS
- Divide and Conquer

### Week 6: DP & Misc
- Kadane's
- 1D DP
- 2D DP
- Bit Manipulation
- Math

### Daily routine (recommended)

1. Read the theory for today's topic (this guide!)
2. Solve 2-3 easy problems in the category
3. Try 1-2 medium problems
4. Review — for each problem, note:
   - What pattern did it match?
   - What was the trick?
   - What did I get wrong the first time?

**Golden rule**: DON'T look at the solution until you've tried for 20-30 minutes. Struggling is where learning happens.

Good luck! You've got this. 🚀
