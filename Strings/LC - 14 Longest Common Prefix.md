**📁 Folder:** `Strings`

**File Name:** `LC - 14 Longest Common Prefix.md`

# 🧩 LeetCode 14 - Longest Common Prefix

## 🔗 Problem

[LeetCode - Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/)

---

## 🏷️ Tags

* String
* Sorting

---

## 📚 Topics

* String Comparison
* Lexicographical Sorting
* Common Prefix

---

## 📊 Difficulty

Easy

---

## 💡 Intuition

We need to find the **longest prefix common to all strings**.

For example:

```text
strs = ["flower", "flow", "flight"]
```

Common prefix:

```text
"fl"
```

A useful observation is:

> After sorting the strings lexicographically, we only need to compare the **first and last strings**.

Why?

Because the first and last strings will have the **maximum difference** in their characters.

If they have a common prefix, then every string between them must also have that prefix.

```text
["flower", "flow", "flight"]
```

After sorting:

```text
["flight", "flow", "flower"]
```

Compare:

```text
flight
flower
 ↑
 f → same
 l → same
 i ≠ o
```

Therefore:

```text
"fl"
```

is the longest common prefix.

---

## 🧠 Thought Process

First:

```java
Arrays.sort(strs);
```

After sorting:

```text
first string  → strs[0]
last string   → strs[strs.length - 1]
```

We compare these two strings character by character.

```java
if(strs[0].charAt(i) != strs[strs.length-1].charAt(i))
```

If the characters are different, the common prefix ends at `i`.

So we return:

```java
strs[0].substring(0, i);
```

If we finish the entire loop without finding a mismatch, then the first string itself is the common prefix.

---

## 🔍 Dry Run

### Example

```text
strs = ["flower", "flow", "flight"]
```

After sorting:

```text
["flight", "flow", "flower"]
```

Compare first and last:

```text
flight
flower
```

### Character comparison

| `i` | First | Last | Result    |
| --: | :---: | :--: | --------- |
|   0 |  `f`  |  `f` | Same      |
|   1 |  `l`  |  `l` | Same      |
|   2 |  `i`  |  `o` | Different |

At:

```text
i = 2
```

we have a mismatch.

Therefore:

```java
strs[0].substring(0, 2)
```

returns:

```text
"fl"
```

---

## ⭐ Main Logic

The whole solution is based on this idea:

```text
Sort the strings
      ↓
Take first and last
      ↓
Compare characters
      ↓
First mismatch
      ↓
Return prefix before mismatch
```

### Why only first and last?

Suppose:

```text
["abc", "abcd", "abce", "abcf"]
```

After sorting, the first and last are:

```text
abc
abcf
```

If these two strings agree on:

```text
"abc"
```

then every string between them must also start with `"abc"`.

So checking the extremes is enough.

---

## 🎯 Key Pattern

### Sorting + Extreme Comparison

This is a useful String pattern:

```text
Sort
 ↓
Compare minimum and maximum
 ↓
Find common part
```

For this problem:

```text
First string + Last string
        ↓
Character-by-character comparison
        ↓
Longest Common Prefix
```

---

## 💻 Java Solution

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        Arrays.sort(strs);

        for(int i = 0; i < strs[0].length(); i++){

            if(strs[0].charAt(i) != strs[strs.length-1].charAt(i)){
                return strs[0].substring(0, i);
            }

        }

        return strs[0];
    }
}
```

---

## 🧪 Another Example

```text
strs = ["dog", "racecar", "car"]
```

After sorting:

```text
["car", "dog", "racecar"]
```

Compare:

```text
car
racecar
```

First characters:

```text
c ≠ r
```

Mismatch at `i = 0`.

Therefore:

```text
""
```

is returned.

---

## ⏱️ Complexity

### Time Complexity

```text
O(n log n × m)
```

Sorting the strings takes `O(n log n)` comparisons, and each comparison can involve up to `m` characters.

Then we compare the first and last strings in `O(m)`.

Where:

* `n` = number of strings
* `m` = maximum string length

### Space Complexity

```text
O(1)
```

Apart from the space used internally by Java's sorting implementation.

---

## 📌 Key Takeaways

* Sort the strings first.
* After sorting, compare only the **first and last strings**.
* Find the first character where they differ.
* Everything before that index is the common prefix.
* If there is no mismatch, return the first string.

### 🧠 Pattern to Remember

```text
Strings
   ↓
Sort
   ↓
First + Last
   ↓
Compare characters
   ↓
First mismatch
   ↓
Common Prefix
```
