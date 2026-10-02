**📁 Folder:** `Binary_Search`

**File Name:** `LC - 50 Pow(x, n).md`

# 🧩 Pow(x, n)

## 🔗 Problem

[LeetCode 50 — Pow(x, n)](https://leetcode.com/problems/powx-n/)

---

## 🏷️ Tags

`Math` `Binary Exponentiation` `Recursion` `Iteration`

## 📚 Topics

* Fast Exponentiation
* Binary Exponentiation
* Powers
* Iterative approach

## 📊 Difficulty

**Medium**

---

## 💡 Intuition

The straightforward way to calculate:

```text
xⁿ
```

would be to multiply `x` by itself `n` times.

For example:

```text
2⁵ = 2 × 2 × 2 × 2 × 2
```

That takes **O(n)** time.

But we can do better using **Binary Exponentiation**.

The main idea is:

* If `n` is **even**, we can square `x` and divide `n` by `2`.
* If `n` is **odd**, multiply `ans` by `x` once and reduce `n` by `1`.

For example:

```text
x⁸
```

can become:

```text
x⁸
→ (x²)⁴
→ (x⁴)²
→ (x⁸)¹
```

So the exponent keeps getting divided by `2`, giving **O(log n)** time.

---

## 🧠 Thought Process

### Step 1 — Start with `ans = 1`

```java
double ans = 1.0;
```

We use `ans` to store the part of the answer that we have already calculated.

---

### Step 2 — Convert `n` to `long`

```java
long nn = n;
```

This is important because `n` is an `int`.

The minimum integer value is:

```text
-2147483648
```

If we directly do:

```java
n = -n;
```

it can overflow because `2147483648` cannot be represented by an `int`.

Using `long` allows us to safely store the positive value.

---

### Step 3 — Handle negative exponent

```java
if (n < 0) {
    nn = -nn;
}
```

If:

```text
x⁻ⁿ
```

then:

```text
x⁻ⁿ = 1 / xⁿ
```

So we first calculate the positive power and later take the reciprocal.

---

# ⭐ Main Logic

The important part is:

```java
while (nn > 0) {
    if (nn % 2 == 0) {
        x = x * x;
        nn = nn / 2;
    } else {
        ans = ans * x;
        nn = nn - 1;
    }
}
```

There are two cases.

---

## Case 1 — `nn` is even

```java
if (nn % 2 == 0)
```

Suppose:

```text
x = 2
nn = 8
```

We can write:

```text
2⁸ = (2²)⁴
```

So:

```java
x = x * x;
nn = nn / 2;
```

becomes:

```text
x = 4
nn = 4
```

We have reduced the exponent by half.

---

## Case 2 — `nn` is odd

Suppose:

```text
x = 2
nn = 5
```

We cannot directly divide `5` by `2`.

So first take one `x`:

```text
2⁵ = 2 × 2⁴
```

That's what:

```java
ans = ans * x;
nn = nn - 1;
```

does.

After that:

```text
nn = 4
```

Now it is even, so we can use the squaring step.

---

# 🔍 Dry Run

Let's take:

```text
x = 2
n = 10
```

Expected:

```text
2¹⁰ = 1024
```

Initial:

```text
ans = 1
x = 2
nn = 10
```

### Iteration 1

`nn = 10` → even

```text
x = 2 × 2 = 4
nn = 10 / 2 = 5
ans = 1
```

---

### Iteration 2

`nn = 5` → odd

```text
ans = 1 × 4 = 4
nn = 5 - 1 = 4
```

---

### Iteration 3

`nn = 4` → even

```text
x = 4 × 4 = 16
nn = 4 / 2 = 2
ans = 4
```

---

### Iteration 4

`nn = 2` → even

```text
x = 16 × 16 = 256
nn = 2 / 2 = 1
ans = 4
```

---

### Iteration 5

`nn = 1` → odd

```text
ans = 4 × 256 = 1024
nn = 1 - 1 = 0
```

Loop ends.

```text
ans = 1024
```

So:

```text
2¹⁰ = 1024
```

---

# 🧪 Negative Exponent Example

Suppose:

```text
x = 2
n = -3
```

We first convert:

```text
nn = 3
```

Calculate:

```text
2³ = 8
```

Then:

```java
if (n < 0) {
    ans = 1.0 / ans;
}
```

So:

```text
1 / 8 = 0.125
```

Therefore:

```text
2⁻³ = 0.125
```

---

## 💻 Java Solution

```java
class Solution {
    public double myPow(double x, int n) {
        double ans = 1.0;
        long nn = n;

        if (n < 0) {
            nn = -nn;
        }

        while (nn > 0) {
            if (nn % 2 == 0) {
                x = x * x;
                nn = nn / 2;
            } else {
                ans = ans * x;
                nn = nn - 1;
            }
        }

        if (n < 0) {
            ans = (double) (1.0) / (double) ans;
        }

        return ans;
    }
}
```

---

## 🎯 Key Pattern

### Binary Exponentiation / Fast Power

Remember the flow:

```text
n even
   ↓
square x
divide n by 2

n odd
   ↓
multiply ans by x
decrease n by 1
```

The important observation is:

> **Instead of doing `n` multiplications, repeatedly reduce the exponent.**

---

## ⏱️ Complexity

### Time — `O(log n)`

When `nn` is even, it gets divided by `2`.

So the number of iterations is logarithmic.

### Space — `O(1)`

Only a few variables are used.

---

## 📌 Key Takeaways

* Don't calculate `xⁿ` using `n` repeated multiplications.
* Use **Binary Exponentiation**.
* Even exponent → square `x`, divide exponent by `2`.
* Odd exponent → multiply `ans` by `x`, reduce exponent by `1`.
* Negative exponent → calculate positive power and take reciprocal.
* Use `long` for the exponent to safely handle `Integer.MIN_VALUE`.
* Pattern: **Fast Power / Binary Exponentiation**.
