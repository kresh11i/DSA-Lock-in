**📁 Folder:** `Strings`

**File Name:** `LC - 1021 Remove Outermost Parentheses.md`

# 🧩 LeetCode 1021 - Remove Outermost Parentheses

## 🔗 Problem

[LeetCode - Remove Outermost Parentheses](https://leetcode.com/problems/remove-outermost-parentheses/)

---

## 🏷️ Tags

* String
* Stack
* Parentheses
* Depth Tracking

---

## 📚 Topics

* Balanced Parentheses
* String Traversal
* Depth Tracking
* Nested Structures

---

## 📊 Difficulty

Easy

---

## 💡 Intuition

The string consists of **primitive valid parentheses strings**.

For example:

```text
(()())(()) 
```

can be divided into:

```text
(()())
(()) 
```

For every primitive group, we need to remove its **outermost `(` and `)`**.

Instead of actually separating the primitive groups, we can track the **current depth** of parentheses.

The key idea is:

> The outermost `(` is added when the depth is `0`, and the outermost `)` is encountered when the depth becomes `0`.

So we simply **don't add those characters** to our answer.

---

## 🧠 Thought Process

We maintain:

```text
depth = current nesting level
```

### When we see `(`

If:

```text
depth > 0
```

then this `(` is **not outermost**, so we add it.

Then increase the depth:

```text
depth++;
```

### When we see `)`

First decrease the depth:

```text
depth--;
```

If:

```text
depth > 0
```

then this `)` is **not outermost**, so we add it.

This means:

```text
depth == 0
```

identifies the boundaries of a primitive parentheses group.

---

## 🔍 Dry Run

### Example

```text
s = "(()())(())"
```

Let's track the depth:

| Character | Depth Before | Action    | Depth After |
| --------- | -----------: | --------- | ----------: |
| `(`       |            0 | Don't add |           1 |
| `(`       |            1 | Add       |           2 |
| `)`       |            2 | Add       |           1 |
| `(`       |            1 | Add       |           2 |
| `)`       |            2 | Add       |           1 |
| `)`       |            1 | Don't add |           0 |
| `(`       |            0 | Don't add |           1 |
| `(`       |            1 | Add       |           2 |
| `)`       |            2 | Add       |           1 |
| `)`       |            1 | Don't add |           0 |

The characters added are:

```text
()()
()
```

So the final result is:

```text
()()()
```

---

## ⭐ Main Logic

The most important part is understanding **when to append**.

### For `(`

```java
if(depth > 0){
    ans.append(ch);
}
depth++;
```

If `depth == 0`, it means this is the **outermost opening parenthesis**, so we skip it.

---

### For `)`

```java
depth--;
if(depth > 0){
    ans.append(ch);
}
```

We decrease the depth first.

If the depth becomes `0`, it means we just encountered the **outermost closing parenthesis**, so we skip it.

---

## 🎯 Key Pattern

### Depth Tracking

Whenever you see nested structures such as parentheses, think about maintaining a **depth counter**.

```text
( → depth++

) → depth--
```

Then:

```text
depth = 0
```

means we are outside the current primitive group.

The important observation is:

```text
Opening `(` at depth 0 → outermost → skip

Closing `)` that makes depth 0 → outermost → skip
```

Everything else is part of the inner structure and should be added.

---

## 💻 Java Solution

```java
class Solution {
    public String removeOuterParentheses(String s) {

        StringBuilder ans = new StringBuilder();
        int depth = 0;

        for (char ch : s.toCharArray()) {
            if(ch=='('){
                if(depth>0){
                    ans.append(ch);
                }
                depth++;
            }
            else if(ch==')'){
                depth--;
                if(depth>0){
                    ans.append(ch);
                }
            }
        }

        return ans.toString();
    }
}
```

---

## 🧪 Another Example

```text
s = "(()())"
```

The primitive string is:

```text
(()())
```

Remove the outermost parentheses:

```text
()()
```

So:

```text
Input  → (()())
Output → ()()
```

---

## ⏱️ Complexity

### Time Complexity

```text
O(n)
```

We traverse the string once.

### Space Complexity

```text
O(n)
```

The `StringBuilder` stores the resulting string.

---

## 📌 Key Takeaways

* Use a `depth` variable to track nesting.
* For `(`:

  * Append only if `depth > 0`.
  * Then increase depth.
* For `)`:

  * First decrease depth.
  * Append only if `depth > 0`.
* An opening parenthesis at depth `0` is an **outermost `(`**.
* A closing parenthesis that makes depth `0` is an **outermost `)`**.
* `StringBuilder` is used to efficiently construct the answer.

### 🧠 Pattern to Remember

```text
Parentheses
     ↓
Track depth
     ↓
( → depth++
) → depth--
     ↓
Skip characters at the outermost level
```
