# Palindrome Number

## 🔗 Problem Link

https://leetcode.com/problems/palindrome-number/

## 🏷️ Tags

- Math
- Integer

## 📚 Topics

- Math

## 📊 Difficulty

Easy

## 📖 Problem Statement

Given an integer `x`, return `true` if `x` is a palindrome, and `false` otherwise.

A palindrome number reads the same from left to right and right to left.

---

## ✨ Examples

### Example 1

```text
Input: x = 121

Output: true
```

### Example 2

```text
Input: x = -121

Output: false
```

### Example 3

```text
Input: x = 10

Output: false
```

---

## 🚀 Approach

### Pattern Used

**Mathematical Reversal**

### Intuition

Reverse the given number digit by digit and compare it with the original number.

If both numbers are equal, then the number is a palindrome.

### Why This Approach Works

Reversing the number changes the order of its digits.

- If the reversed number is equal to the original number, it reads the same from both directions.
- Otherwise, it is not a palindrome.

### Algorithm

1. Store the original number.
2. Initialize `rev = 0`.
3. Extract the last digit using `% 10`.
4. Add the digit to the reversed number.
5. Remove the last digit using `/ 10`.
6. Repeat until the number becomes `0`.
7. Compare the original number with the reversed number.
8. Return the result.

---

## 💻 Java Solution

```java
class Solution {
    public boolean isPalindrome(int x) {
        int temp = x;
        int rev = 0;
        boolean result = true;

        while (x > 0) {
            int lastD = x % 10;
            x = x / 10;
            rev = (rev * 10) + lastD;
        }

        if (temp == rev) {
            result = true;
        } else {
            result = false;
        }

        return result;
    }
}
```

---

## ⭐ Main Logic

```java
rev = (rev * 10) + lastD;
```

### Why is this the Main Logic?

This line builds the reversed number.

- Multiply the current reversed number by `10`.
- Add the last extracted digit.
- Repeat until all digits are processed.

> **Interview Takeaway:**  
> Whenever you need to reverse an integer, think of extracting digits using `% 10` and removing digits using `/ 10`.

---

## 🧪 Dry Run

### Input

```text
x = 121
```

### Initial State

```text
temp = 121
rev = 0
```

| x | Last Digit (`x % 10`) | rev | x after `/10` |
|---|------------------------|-----|---------------|
|121|1|1|12|
|12|2|12|1|
|1|1|121|0|

### Comparison

```text
Original Number = 121
Reversed Number = 121
```

Since both are equal,

```text
Output = true
```

---

## ⏱️ Complexity Analysis

### Time Complexity

**O(log₁₀ n)**

- One iteration for each digit of the number.

### Space Complexity

**O(1)**

- Only a few integer variables are used.

---

## 📌 Constraints

- `-2³¹ <= x <= 2³¹ - 1`

---

## 💡 Key Points

- Store the original number.
- Reverse the number digit by digit.
- Compare the reversed number with the original.
- Use `% 10` to extract digits.
- Use `/ 10` to remove digits.
- No extra data structure is required.

---

## ⚠️ Common Mistakes

- Forgetting to store the original number.
- Comparing after modifying the original value.
- Using strings instead of mathematical operations.
- Forgetting that negative numbers are never palindromes.

---

## 📝 Revision Snapshot

**Problem Type:** Number Manipulation

**Pattern Used:** Mathematical Reversal

**Main Data Structure:** Integer

**Main Formula:**

```text
lastDigit = x % 10
rev = (rev * 10) + lastDigit
x = x / 10
```

**Key Idea:**

Reverse the number using mathematical operations and compare it with the original number. If both are equal, the number is a palindrome.