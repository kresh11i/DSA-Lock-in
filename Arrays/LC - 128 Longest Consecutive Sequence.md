**📁 Folder:** `Arrays`

**File Name:** `LC - 128 Longest Consecutive Sequence.md`

# 🧩 Longest Consecutive Sequence

## 🔗 Problem

[LeetCode 128 — Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/)

---

## 🏷️ Tags

`Array` `HashSet` `Hashing`

## 📚 Topics

* HashSet
* Consecutive sequence
* Searching
* Array

## 📊 Difficulty

**Medium**

---

## 💡 Intuition

We need to find the length of the **longest consecutive sequence** in an unsorted array.

Example:

```text
nums = [100, 4, 200, 1, 3, 2]
```

The consecutive sequence is:

```text
1 → 2 → 3 → 4
```

So the answer is:

```text
4
```

The important idea is:

> Put all numbers into a `HashSet` so we can check whether a number exists in **O(1) average time**.

But we should **not start a sequence from every number**.

For a number `num`, check:

```java
set.contains(num - 1)
```

If `num - 1` exists, then `num` is **not the beginning** of a sequence.

If `num - 1` does **not** exist, then `num` is the beginning of a sequence.

---

## 🧠 Thought Process

### Step 1 — Put all numbers into a HashSet

```java
HashSet<Integer> set = new HashSet<>();

for (int num : nums) {
    set.add(num);
}
```

For:

```text
[100, 4, 200, 1, 3, 2]
```

we get:

```text
{100, 4, 200, 1, 3, 2}
```

Now checking whether a number exists is fast.

---

### Step 2 — Find the beginning of a sequence

```java
if (!set.contains(num - 1))
```

This is the key condition.

For `1`:

```text
0 doesn't exist
```

So `1` is the beginning.

For `2`:

```text
1 exists
```

So `2` is **not** the beginning.

For `3`:

```text
2 exists
```

Not the beginning.

For `4`:

```text
3 exists
```

Not the beginning.

Therefore, we only start counting from `1`.

---

### Step 3 — Expand the sequence

Once we find a starting number:

```java
int start = num;
int match = 1;
```

Then:

```java
while (set.contains(start + 1)) {
    start++;
    match++;
}
```

For `1`:

```text
1 → 2 → 3 → 4
```

So:

```text
match = 4
```

---

### Step 4 — Keep the longest sequence

```java
longest = Math.max(longest, match);
```

If the current sequence is longer than the previous answer, update `longest`.

---

## 🔍 Dry Run

### Input

```text
nums = [100, 4, 200, 1, 3, 2]
```

After creating the set:

```text
{100, 4, 200, 1, 3, 2}
```

---

### `num = 100`

Check:

```text
99 exists? ❌
```

So `100` is a sequence starting point.

```text
100
```

`match = 1`

```text
101 exists? ❌
```

So:

```text
longest = 1
```

---

### `num = 4`

Check:

```text
3 exists? ✅
```

So `4` is not a starting point.

Skip it.

---

### `num = 200`

Check:

```text
199 exists? ❌
```

Start sequence:

```text
200
```

`201` doesn't exist.

So:

```text
longest = 1
```

---

### `num = 1`

Check:

```text
0 exists? ❌
```

So `1` is a starting point.

Start:

```text
1
```

Check:

```text
2 exists? ✅
```

```text
1 → 2
match = 2
```

Check:

```text
3 exists? ✅
```

```text
1 → 2 → 3
match = 3
```

Check:

```text
4 exists? ✅
```

```text
1 → 2 → 3 → 4
match = 4
```

Check:

```text
5 exists? ❌
```

Stop.

Now:

```text
longest = Math.max(1, 4)
       = 4
```

---

### `num = 3`

Check:

```text
2 exists? ✅
```

Not a starting point.

Skip.

---

### `num = 2`

Check:

```text
1 exists? ✅
```

Not a starting point.

Skip.

---

## ✅ Final Answer

```text
4
```

The longest consecutive sequence is:

```text
1 → 2 → 3 → 4
```

---

## ⭐ Main Logic

The most important part is:

```java
if (!set.contains(num - 1)) {
```

This prevents us from repeatedly counting the same sequence.

Without this condition:

```text
1 → 2 → 3 → 4
2 → 3 → 4
3 → 4
4
```

We would repeatedly traverse the same sequence.

Instead:

```text
Only start when num - 1 doesn't exist
```

So:

```text
1 → start
2 → skip
3 → skip
4 → skip
```

---

## 🎯 Key Pattern

### HashSet + Sequence Start Detection

Remember this pattern:

```text
Put everything into HashSet
        ↓
Find numbers with NO predecessor
        ↓
Start sequence from there
        ↓
Keep checking num + 1
        ↓
Track maximum length
```

The two important checks are:

```java
!set.contains(num - 1)
```

and

```java
set.contains(start + 1)
```

---

## 💻 Java Solution

Your code has one missing declaration: `longest` needs to be initialized before it is used.

```java
class Solution {
    public int longestConsecutive(int[] nums) {
        HashSet<Integer> set = new HashSet<>();
        int longest = 0;

        for (int num : nums) {
            set.add(num);
        }

        for (int num : set) {
            if (!set.contains(num - 1)) {
                int start = num;
                int match = 1;

                while (set.contains(start + 1)) {
                    start++;
                    match++;
                }

                longest = Math.max(longest, match);
            }
        }

        return longest;
    }
}
```

### ⚠️ Your code's only issue

You used:

```java
longest = Math.max(longest, match);
```

but `longest` was never declared.

You need:

```java
int longest = 0;
```

Everything else follows the correct **HashSet + sequence-start** approach.

---

## ⏱️ Complexity

### Time — `O(n)` average

* Insert all `n` elements into the HashSet → `O(n)`
* Each number is considered as a sequence start only when `num - 1` doesn't exist.
* Each consecutive sequence is traversed once.

Overall average:

```text
O(n)
```

### Space — `O(n)`

The HashSet stores the elements.

---

## 📌 Key Takeaways

* Use a `HashSet` for fast existence checks.
* A number is a **sequence start** if `num - 1` doesn't exist.
* From the start, keep checking `num + 1`.
* Don't start counting from numbers that already have a predecessor.
* This avoids sorting and achieves **O(n) average time**.
* Pattern: **HashSet + Sequence Start Detection**.
