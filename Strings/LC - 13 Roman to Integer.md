**📁 Folder:** `Strings`

**File Name:** `LC - 13 Roman to Integer.md`

# 🧩 Roman to Integer

## 🔗 Problem

[LeetCode 13 — Roman to Integer](https://leetcode.com/problems/roman-to-integer/)

---

## 🏷️ Tags

`String` `Hashing` `Switch` `Greedy`

## 📚 Topics

* Roman numeral conversion
* String traversal
* Comparing adjacent characters
* Subtraction logic

## 📊 Difficulty

**Easy**

---

## 💡 Intuition

Roman numerals normally work by adding their values.

For example:

* `VI` → `5 + 1 = 6`
* `XV` → `10 + 5 = 15`

But there are special cases where a **smaller value comes before a larger value**, meaning we have to subtract it.

Examples:

* `IV` → `5 - 1 = 4`
* `IX` → `10 - 1 = 9`
* `XL` → `50 - 10 = 40`

So while traversing the string:

* If `current < next` → subtract `current`
* Otherwise → add `current`

For the **last character**, there is no next character to compare with, so we simply add its value.

---

## 🧠 Thought Process

I maintain three variables:

* `current` → value of the current Roman character
* `next` → value of the next Roman character
* `ans` → final answer

For every character except the last one:

1. Convert the current character into its numerical value.
2. Convert the next character into its numerical value.
3. Compare them.
4. If current is smaller, subtract it.
5. Otherwise, add it.

After the loop, add the value of the last character.

### Example: `MCMIV`

```text
M C M I V
1000 100 1000 1 5
```

* `M < C` → false → `+1000`
* `C < M` → true → `-100`
* `M < I` → false → `+1000`
* `I < V` → true → `-1`
* Last `V` → `+5`

```text
1000 - 100 + 1000 - 1 + 5
= 1904
```

---

## 🔍 Dry Run

### Input

`IV`

| Current |  Next | Comparison     | Action | ans |
| ------- | ----: | -------------- | -----: | --: |
| I = 1   | V = 5 | 1 < 5          |   `-1` |  -1 |
| V = 5   |     — | Last character |   `+5` |   4 |

### Output

`4`

---

## 💻 Java Solution

```java
class Solution { 
    public int romanToInt(String s) { 
        int ans = 0, next = 0, current = 0; 

        for (int i = 0; i < s.length()-1; i++) { 

            switch (s.charAt(i)) { 
                case 'I': 
                    current = 1; 
                    break; 
                case 'V': 
                    current = 5; 
                    break; 
                case 'X': 
                    current = 10; 
                    break; 
                case 'L': 
                    current = 50; 
                    break; 
                case 'C': 
                    current = 100; 
                    break; 
                case 'D': 
                    current = 500; 
                    break; 
                case 'M': 
                    current = 1000; 
                    break; 
            } 
 
            switch (s.charAt(i + 1)) { 
                case 'I': 
                    next = 1; 
                    break; 
                case 'V': 
                    next = 5; 
                    break; 
                case 'X': 
                    next = 10; 
                    break; 
                case 'L': 
                    next = 50; 
                    break; 
                case 'C': 
                    next = 100; 
                    break; 
                case 'D': 
                    next = 500; 
                    break; 
                case 'M': 
                    next = 1000; 
                    break; 
            } 
 
            if (current < next) { 
                ans -= current; 
            } else { 
                ans += current; 
            } 
        } 

        switch (s.charAt(s.length() - 1)) { 
            case 'I': 
                ans += 1; 
                break; 
            case 'V': 
                ans += 5; 
                break; 
            case 'X': 
                ans += 10; 
                break; 
            case 'L': 
                ans += 50; 
                break; 
            case 'C': 
                ans += 100; 
                break; 
            case 'D': 
                ans += 500; 
                break; 
            case 'M': 
                ans += 1000; 
                break; 
        } 

        return ans; 
    } 
}
```

---

## ⭐ Main Logic

The main condition is:

```java
if (current < next) {
    ans -= current;
} else {
    ans += current;
}
```

This single comparison handles the Roman numeral subtraction cases.

### Remember:

```text
Smaller → Larger  → Subtract
Larger  → Smaller → Add
Same    → Same     → Add
```

---

## 🎯 Key Pattern

**Adjacent comparison + greedy addition/subtraction**

Instead of explicitly checking for:

```text
IV
IX
XL
XC
CD
CM
```

we simply compare the current value with the next value.

---

## ⏱️ Complexity

### Time

**O(n)**

We traverse the string once.

### Space

**O(1)**

Only a few integer variables are used.

---

## 📌 Key Takeaways

* Roman characters can be converted into numerical values.
* Compare the **current value with the next value**.
* If `current < next`, subtract it.
* Otherwise, add it.
* The last character is always added separately.
* This avoids explicitly checking every subtraction combination.
