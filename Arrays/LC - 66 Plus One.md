**📁 Folder:** `Arrays`

**File Name:** `LC - 66 Plus One.md`

# 🧩 LeetCode 66 - Plus One

## 🔗 Problem

[LeetCode - Plus One](https://leetcode.com/problems/plus-one/)

---

## 🏷️ Tags

* Array
* Math

---

## 📚 Topics

* Array Traversal
* Carry
* Digit Manipulation

---

## 📊 Difficulty

Easy

---

## 💡 Intuition

The array represents a number where each element is a digit.

For example:

```text
digits = [1, 2, 3]
```

represents:

```text
123
```

We need to add `1`:

```text
123 + 1 = 124
```

The important thing is that addition starts from the **last digit**, just like normal addition.

### What happens with `9`?

If the last digit is `9`:

```text
[1, 2, 9]
```

Adding `1` gives:

```text
[1, 3, 0]
```

So:

```text
9 → 0
```

and the carry moves to the previous digit.

If we have:

```text
[9, 9, 9]
```

all digits become `0`, and we need one extra digit:

```text
[1, 0, 0, 0]
```

---

## 🧠 Thought Process

Start from:

```text
digits.length - 1
```

and move towards the beginning.

For every digit:

### Case 1: Digit is `9`

```text
digits[i] == 9
```

We cannot directly add `1` because:

```text
9 + 1 = 10
```

So:

```java
digits[i] = 0;
```

and continue towards the left.

### Case 2: Digit is not `9`

We can simply increment it:

```java
digits[i] += 1;
```

Then we are done, so:

```java
return digits;
```

### Case 3: Every digit was `9`

If the loop finishes, it means the original number was something like:

```text
9
99
999
```

So we need an extra digit.

That's why:

```java
int[] ans = new int[digits.length + 1];
ans[0] = 1;
```

creates:

```text
[1, 0, 0, ...]
```

---

## 🔍 Dry Run

### Example 1

```text
digits = [1, 2, 3]
```

Start from the right:

```text
3 != 9
```

Increment:

```text
3 → 4
```

Return immediately:

```text
[1, 2, 4]
```

---

### Example 2

```text
digits = [1, 2, 9]
```

Start:

```text
9 == 9
```

Set:

```text
9 → 0
```

Array:

```text
[1, 2, 0]
```

Move left:

```text
2 != 9
```

Increment:

```text
2 → 3
```

Return:

```text
[1, 3, 0]
```

---

### Example 3

```text
digits = [9, 9, 9]
```

Process from right:

```text
9 → 0
9 → 0
9 → 0
```

Array becomes:

```text
[0, 0, 0]
```

The loop finishes without returning.

So:

```java
int[] ans = new int[digits.length + 1];
ans[0] = 1;
```

creates:

```text
[1, 0, 0, 0]
```

Return:

```text
[1, 0, 0, 0]
```

---

## ⭐ Main Logic

The core idea is **carry propagation from right to left**.

```text
Start from last digit
        ↓
Is it 9?
   ↙         ↘
 YES          NO
  ↓            ↓
Set to 0    Add 1
  ↓            ↓
Move left    DONE
```

The moment we find a digit that is not `9`, the carry stops.

For example:

```text
[4, 9, 9]
```

Processing:

```text
9 → 0
9 → 0
4 → 5
```

Result:

```text
[5, 0, 0]
```

---

## 🎯 Key Pattern

### Carry Propagation

This is the same concept used in normal addition.

```text
129 + 1
```

Start from the right:

```text
9 + 1 = 10
```

So:

```text
9 → 0
carry → left
```

Then:

```text
2 + 1 = 3
```

So:

```text
[1, 3, 0]
```

In the array solution, we simulate exactly this process.

---

## 💻 Java Solution

```java
class Solution {
    public int[] plusOne(int[] digits) {
        int[] ans = new int[digits.length + 1];
        ans[0] = 1;

        for (int i = digits.length - 1; i >= 0; i--) {
            if (digits[i] == 9) {
                digits[i] = 0;

            } else {
                digits[i] += 1;
                return digits;

            }
        }

        return ans;
    }
}
```

---

## 🧪 Another Example

```text
Input:
[4, 9, 9]

Right → Left:

9 → 0
9 → 0
4 → 5

Output:
[5, 0, 0]
```

Another:

```text
Input:
[8]

8 + 1 = 9

Output:
[9]
```

---

## ⏱️ Complexity

### Time Complexity

```text
O(n)
```

In the worst case, every digit can be `9`, so we traverse the entire array.

### Space Complexity

```text
O(n)
```

In the all-`9` case, we create a new array of size `n + 1`.

Otherwise, the input array is modified directly.

---

## 📌 Key Takeaways

* Addition starts from the **rightmost digit**.
* If digit is `9`:

  * Change it to `0`.
  * Continue carrying left.
* If digit is not `9`:

  * Increment it.
  * Return immediately.
* If every digit is `9`, create an array of size `n + 1` and put `1` at index `0`.

### 🧠 Pattern to Remember

```text
Add 1
  ↓
Start from right
  ↓
9 → 0 → carry left
  ↓
non-9 → +1 → stop
  ↓
all 9s → [1, 0, 0, ...]
```
