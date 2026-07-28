# Reverse String

## 🔗 Problem Link

https://leetcode.com/problems/reverse-string/

## 🏷️ Tags

- String
- Two Pointer
- In-Place

## 📚 Topics

- Two Pointers
- String

## 📊 Difficulty

Easy

## 📖 Problem Statement

Write a function that reverses a string.

The input is given as an array of characters `s`.

Modify the array in-place using **O(1)** extra memory.

---

## ✨ Examples

### Example 1

```text
Input: s = ["h","e","l","l","o"]

Output: ["o","l","l","e","h"]
```

### Example 2

```text
Input: s = ["H","a","n","n","a","h"]

Output: ["h","a","n","n","a","H"]
```

---

## 🚀 Approach

### Pattern Used

**Two Pointers (Single Pointer Implementation)**

### Intuition

Normally, this problem is solved using two pointers:

- Left pointer starts from the beginning.
- Right pointer starts from the end.

In my solution, I used only **one pointer** (`i`).

Instead of maintaining another pointer, I calculate the last index every time using:

```text
s.length - i - 1
```

Then I swap the current character with its corresponding character from the end.

### Why This Approach Works

As `i` moves from left to right, the expression

```text
s.length - i - 1
```

automatically gives the matching index from the right side.

The loop runs only until the middle of the array, so every character is swapped exactly once.

### Algorithm

1. Start from the first character.
2. Find the corresponding last index using `s.length - i - 1`.
3. Swap both characters.
4. Increment `i`.
5. Stop when the middle of the array is reached.

---

## 💻 Java Solution

```java
class Solution {
    public void reverseString(char[] s) {
        char i = 0;

        while(i < s.length / 2){

            char temp = s[s.length - i - 1];
            s[s.length - i - 1] = s[i];
            s[i] = temp;

            i++;
        }
    }
}
```

---

## ⭐ Main Logic

```java
temp = s[s.length - i - 1];
s[s.length - i - 1] = s[i];
s[i] = temp;
```

### Why is this the Main Logic?

These three lines perform the swap.

Instead of storing a separate right pointer, the last index is calculated using:

```text
s.length - i - 1
```

This allows the string to be reversed using only one pointer variable.

> **Interview Takeaway:**  
> Even if you don't explicitly use a right pointer, calculating `s.length - i - 1` is logically equivalent to having one.

---

## 🧪 Dry Run

### Input

```text
s = ['h','e','l','l','o']
```

### Initial State

```text
Length = 5
Middle = 2
```

| i | Last Index (`length-i-1`) | Swap | Array |
|---|---------------------------|------|-------|
|0|4|h ↔ o|[o,e,l,l,h]|
|1|3|e ↔ l|[o,l,l,e,h]|

Loop stops because

```text
i = 2

2 < 2 ❌ False
```

### Final Output

```text
[o,l,l,e,h]
```

---

## ⏱️ Complexity Analysis

### Time Complexity

**O(n)**

- Only half of the array is traversed.

### Space Complexity

**O(1)**

- Only one temporary variable is used.

---

## 📌 Constraints

- `1 <= s.length <= 10⁵`
- `s[i]` is a printable ASCII character.

---

## 💡 Key Points

- Reverse the string in-place.
- Swap the first and last characters.
- Continue until the middle.
- `s.length - i - 1` gives the matching index from the end.
- No extra array is required.

---

## ⚠️ Common Mistakes

- Forgetting the `-1` while calculating the last index.
- Traversing the entire array instead of stopping at the middle.
- Forgetting to use a temporary variable while swapping.
- Creating another array instead of modifying the original array.

---

## 📝 Revision Snapshot

**Problem Type:** String Manipulation

**Pattern Used:** Two Pointers

**Main Data Structure:** Character Array

**Main Formula:**

```text
Last Index = s.length - i - 1
```

**Key Idea:**

Move from the beginning of the array and calculate the matching index from the end using `s.length - i - 1`. Swap both characters until reaching the middle.