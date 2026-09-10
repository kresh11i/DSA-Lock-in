**📁 Folder:** `Strings`

**File Name:** `LC - 1903 Largest Odd Number in String.md`

# 🧩 LeetCode 1903 - Largest Odd Number in String

## 🔗 Problem

[LeetCode - Largest Odd Number in String](https://leetcode.com/problems/largest-odd-number-in-string/)

---

## 🏷️ Tags

* String
* Greedy

---

## 📚 Topics

* String Traversal
* Greedy
* Substring
* Odd/Even Numbers

---

## 📊 Difficulty

Easy

---

## 💡 Intuition

We are given a string representing a positive integer.

We need to find the **largest-valued odd integer** that is a **non-empty substring starting from index `0`**.

The important observation is:

> A number is odd if and only if its **last digit is odd**.

So instead of checking every possible substring, we can start from the **last digit** and move backwards.

For example:

```text
num = "35420"
```

The last digit is:

```text
0 → even
```

Move left:

```text
2 → even
```

Move left:

```text
4 → even
```

Move left:

```text
5 → odd
```

Therefore:

```text
"35420"
   ↑
   5
```

The largest odd number is:

```text
"35"
```

---

## 🧠 Thought Process

Why do we start from the right?

Because we want the **largest possible prefix** that forms an odd number.

The more digits we keep, the larger the number can be.

So we want to find the **rightmost odd digit**.

Once we find it at index `i`:

```text
num.substring(0, i + 1)
```

gives us the largest possible odd prefix.

### What if there is no odd digit?

Then every digit is even.

Therefore, no odd number can be formed.

Return:

```text
""
```

---

## 🔍 Dry Run

### Example

```text
num = "35420"
```

Start:

```text
i = 4
num.charAt(4) = '0'
```

`0` is even → move left.

```text
i = 3
num.charAt(3) = '2'
```

`2` is even → move left.

```text
i = 2
num.charAt(2) = '4'
```

`4` is even → move left.

```text
i = 1
num.charAt(1) = '5'
```

`5` is odd.

So return:

```text
num.substring(0, 2)
```

which gives:

```text
"35"
```

---

## ⭐ Main Logic

The entire solution revolves around finding the **rightmost odd digit**.

```text
Start from last digit
        ↓
Is digit odd?
   ↙          ↘
 YES           NO
  ↓             ↓
Return      Move left
prefix
```

Once an odd digit is found at index `i`:

```java
return num.substring(0, i + 1);
```

Why `i + 1`?

Because the ending index of `substring()` is exclusive.

For example:

```text
num = "35420"
i = 1
```

Then:

```java
num.substring(0, 2)
```

returns:

```text
"35"
```

---

## 🎯 Key Pattern

### Greedy + Right-to-Left Traversal

We greedily keep the **longest possible prefix**.

The rightmost odd digit gives us the longest prefix whose last digit is odd.

So the pattern is:

```text
Find the rightmost position satisfying a condition
        ↓
Return everything before that position
```

Here the condition is:

```text
digit is odd
```

---

## 💻 Java Solution

```java
class Solution {

    public String largestOddNumber(String num) {

        int i = num.length()-1;

        while(i>=0){

            if(num.charAt(i) %2!=0){

                return num.substring(0,i+1);

            }else{

                i--;

            }
        }

        return "";
    }

}
```

---

## 🧪 Another Example

```text
Input:
"52"

Start from the right:

2 → even

Move left:

5 → odd
```

Return:

```text
"5"
```

### Another Example

```text
Input:
"2468"
```

All digits are even.

Therefore:

```text
Output:
""
```

---

## ⏱️ Complexity

### Time Complexity

```text
O(n)
```

In the worst case, we may traverse the entire string.

### Space Complexity

```text
O(n)
```

`substring()` creates the resulting string.

---

## 📌 Key Takeaways

* A number is odd based only on its **last digit**.
* Start from the **rightmost digit**.
* Find the first odd digit while moving backwards.
* Return the prefix ending at that digit.
* If no odd digit exists, return `""`.
* This is a simple **Greedy** approach.

### 🧠 Pattern to Remember

```text
Need largest odd prefix
        ↓
Odd number depends on last digit
        ↓
Start from the right
        ↓
Find rightmost odd digit
        ↓
Return prefix
```
