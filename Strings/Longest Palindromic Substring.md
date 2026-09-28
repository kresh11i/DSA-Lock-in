# 🧩 LC 5 — Longest Palindromic Substring

Your approach is **Expand Around Center**.

The main idea is simple:

> Every palindrome has a center. Start from every possible center and expand outward while the characters match.

There are **2 types of centers**:

1. **Odd-length palindrome** → one center character
   Example: `aba`
2. **Even-length palindrome** → center is between two characters
   Example: `abba`

Your code checks **both** for every `i`.

---

## 🧠 First Understand the Core Idea

Suppose:

```text
s = "babad"
```

For the palindrome:

```text
  b a b
    ↑
   center
```

Start at `a` and expand:

```text
L = a
R = a
```

Compare:

```text
s[L] == s[R] → a == a ✅
```

Expand:

```text
L → b
R → b
```

Again:

```text
b == b ✅
```

Expand again:

```text
L → outside
R → outside
```

Stop.

So we found:

```text
"bab"
```

---

# 🔍 Now Understand Your Code

### 1. Initial variables

```java
int len = s.length();
int start = 0, maxLen = 1;
```

* `len` → length of string
* `start` → starting index of the longest palindrome found
* `maxLen` → length of the longest palindrome found

Initially:

```text
start = 0
maxLen = 1
```

We assume at least one character is a palindrome.

---

# ⭐ Part 1 — Odd-Length Palindrome

```java
int L = i, R = i;
```

Both pointers start at the **same character**.

Example:

```text
b a b
  ↑
 L,R
```

This checks palindromes like:

```text
a
aba
abcba
```

Then:

```java
while (L >= 0 && R < s.length() && s.charAt(L) == s.charAt(R))
```

There are 3 conditions:

### `L >= 0`

Don't go outside the left side.

### `R < s.length()`

Don't go outside the right side.

### `s.charAt(L) == s.charAt(R)`

The characters must match.

If all are true:

```java
L--;
R++;
```

Expand outward.

---

## ⭐ How is length calculated?

After the `while` loop stops:

```java
int currentLen = R - L - 1;
```

This looks weird initially, but it's important.

The pointers have already moved **one step outside** the palindrome.

Example:

```text
b a b
0 1 2
```

After expansion:

```text
L = -1
R = 3
```

Actual palindrome is indices:

```text
0 → 2
```

Length:

```text
R - L - 1
= 3 - (-1) - 1
= 3
```

So:

```java
start = L + 1;
```

gives:

```text
-1 + 1 = 0
```

which is the actual starting index.

---

# ⭐ Part 2 — Even-Length Palindrome

After checking odd palindrome, your code does:

```java
L = i;
R = i + 1;
```

Now the pointers start **between two characters**.

Example:

```text
a b b a
  ↑ ↑
  L R
```

This allows us to detect:

```text
bb
abba
```

The same expansion logic is used:

```java
while (L >= 0 && R < s.length() && s.charAt(L) == s.charAt(R)) {
    L--;
    R++;
}
```

Then:

```java
int currLen = R - L - 1;
```

and update the answer if this palindrome is longer.

---

# 🧪 Full Dry Run

Let's use:

```text
s = "babad"
```

Indexes:

```text
0 1 2 3 4
b a b a d
```

---

## 🔵 i = 0

Character:

```text
b
```

### Odd palindrome

```text
L = 0
R = 0
```

Compare:

```text
b == b ✅
```

Expand:

```text
L = -1
R = 1
```

Stop because `L < 0`.

Length:

```text
currentLen = R - L - 1
           = 1 - (-1) - 1
           = 1
```

So:

```text
"b"
```

`maxLen = 1`, so no update.

### Even palindrome

```text
L = 0
R = 1
```

Compare:

```text
b != a ❌
```

Stop.

Length = `0`.

Nothing changes.

---

# 🔵 i = 1

Character:

```text
a
```

### Odd palindrome

```text
L = 1
R = 1
```

Compare:

```text
a == a ✅
```

Expand:

```text
L = 0
R = 2
```

Compare:

```text
b == b ✅
```

Expand:

```text
L = -1
R = 3
```

Stop.

Palindrome:

```text
b a b
```

Length:

```text
3 - (-1) - 1 = 3
```

So:

```java
maxLen = 3;
start = 0;
```

Current answer:

```text
"bab"
```

### Even palindrome

Reset:

```text
L = 1
R = 2
```

Compare:

```text
a != b ❌
```

Nothing changes.

---

# 🔵 i = 2

Character:

```text
b
```

### Odd palindrome

```text
L = 2
R = 2
```

Compare:

```text
b == b ✅
```

Expand:

```text
L = 1
R = 3
```

Compare:

```text
a == a ✅
```

Expand:

```text
L = 0
R = 4
```

Compare:

```text
b != d ❌
```

Stop.

We found:

```text
"aba"
```

Length:

```text
4 - 0 - 1 = 3
```

But:

```text
3 > maxLen?
3 > 3 ❌
```

So we keep:

```text
"bab"
```

### Even palindrome

```text
L = 2
R = 3
```

```text
b != a ❌
```

Nothing changes.

---

# 🔵 i = 3

Character:

```text
a
```

### Odd palindrome

```text
L = 3
R = 3
```

```text
a == a ✅
```

Expand:

```text
L = 2
R = 4
```

```text
b != d ❌
```

Palindrome:

```text
"a"
```

Length = `1`.

No update.

### Even palindrome

```text
L = 3
R = 4
```

```text
a != d ❌
```

No update.

---

# 🔵 i = 4

Character:

```text
d
```

### Odd

```text
L = 4
R = 4
```

`d == d`

Expand outside.

Length = `1`.

### Even

```text
L = 4
R = 5
```

Out of bounds.

Nothing changes.

---

# ✅ Final Result

Throughout the process:

```text
maxLen = 3
start = 0
```

Finally:

```java
return s.substring(start, start + maxLen);
```

becomes:

```java
return s.substring(0, 3);
```

Result:

```text
"bab"
```

---

# 🧠 The Most Important Thing to Remember

Your entire solution can be understood as:

```text
For every index i:

        Check odd palindrome
              ↓
          i ← → i

        Check even palindrome
              ↓
         i ← → i+1
```

Then:

```text
Expand while characters match
            ↓
      calculate length
            ↓
   if longer → save it
```

---

## 🎯 Why Two Checks?

This is the **most important concept in this problem**.

### Odd palindrome

```text
   b
  aba
 abcba
```

Center is **one character**:

```text
L = i
R = i
```

### Even palindrome

```text
bb
abba
```

Center is **between two characters**:

```text
L = i
R = i + 1
```

If you only check `L = i, R = i`, you'll completely miss even-length palindromes like `"bb"` and `"abba"`.

---

## ⏱️ Complexity

### Time: **O(n²)**

There are `n` possible centers, and from each center we can expand up to `O(n)` characters.

```text
n centers × n expansion = O(n²)
```

### Space: **O(1)**

Apart from the returned substring, only a few variables are used.

---

## 🔑 Pattern to Remember

**Expand Around Center**

Whenever you see:

> "Find the longest palindrome"

one approach to immediately think of is:

```text
Every palindrome has a center
        ↓
Try every center
        ↓
Expand left and right
        ↓
Keep the longest
```

And remember:

```text
Odd  → L = i, R = i
Even → L = i, R = i + 1
```
