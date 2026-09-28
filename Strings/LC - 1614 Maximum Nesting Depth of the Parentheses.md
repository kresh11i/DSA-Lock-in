**📁 Folder:** `Strings`

**File Name:** `LC - 1614 Maximum Nesting Depth of the Parentheses.md`

# 🧩 LeetCode 1614 - Maximum Nesting Depth of the Parentheses

## 🔗 Problem

[LeetCode - Maximum Nesting Depth of the Parentheses](https://leetcode.com/problems/maximum-nesting-depth-of-the-parentheses/)

---

## 🏷️ Tags

* String
* Stack
* Parentheses

---

## 📚 Topics

* Depth Tracking
* String Traversal
* Nested Parentheses
* Maximum Depth

---

## 📊 Difficulty

Easy

---

## 💡 Intuition

We need to find the **maximum nesting depth** of parentheses in the string.

For example:

```text
(1+(2*3)+((8)/4))+1
```

The deepest nested part is:

```text
((8)/4)
```

Its depth is `2`.

The main idea is simple:

* When we see `(` → increase `depth`.
* When we see `)` → decrease `depth`.
* Every time we increase the depth, check whether it is the maximum we've seen.

So we only need one variable to track the **current depth** and another for the **maximum depth**.

---

## 🧠 Thought Process

Start with:

```text
depth = 0
maxDepth = 0
```

Whenever we encounter:

```text
(
```

we enter one more level:

```text
depth++;
```

Then update:

```text
maxDepth = Math.max(depth, maxDepth);
```

When we encounter:

```text
)
```

we leave one level:

```text
depth--;
```

The maximum value that `depth` reaches during the traversal is our answer.

---

## 🔍 Dry Run

### Example

```text
s = "(1+(2*3)+((8)/4))+1"
```

Track only the parentheses:

```text
(
 → depth = 1
 → maxDepth = 1

(
 → depth = 2
 → maxDepth = 2

)
 → depth = 1

(
 → depth = 2
 → maxDepth = 2

(
 → depth = 3
 → maxDepth = 3

)
 → depth = 2

)
 → depth = 1

)
 → depth = 0
```

Therefore:

```text
maxDepth = 3
```

---

## ⭐ Main Logic

The important part of the solution is:

```java
if(ch == '('){
    depth++;
    maxDepth = Math.max(depth, maxDepth);
}
else if(ch == ')'){
    depth--;
}
```

Think of `depth` like entering and leaving rooms:

```text
(
 ↓
Enter one level
 ↓
depth++

)
 ↓
Leave one level
 ↓
depth--
```

And `maxDepth` simply remembers the deepest level we ever reached.

---

## 🎯 Key Pattern

### Depth Tracking

This is the same **depth tracking** pattern used in other parentheses problems.

```text
( → depth++
) → depth--
```

For maximum depth:

```text
maxDepth = max(maxDepth, depth)
```

So whenever you see a problem involving:

* Nested parentheses
* Nested structures
* Maximum nesting
* Current level/depth

think about maintaining a **depth counter**.

---

## 💻 Java Solution

```java
class Solution {
    public int maxDepth(String s) {
        int depth = 0,maxDepth = 0;
        StringBuilder ans = new StringBuilder();

        for(char ch : s.toCharArray()){
            if(ch == '('){
                if(depth>0){
                    ans.append(ch);
                }

                depth++;
                maxDepth = Math.max(depth,maxDepth);

            }else if( ch == ')'){
                depth--;

                if(depth>0){
                    ans.append(ch);
                }
            }
        }

        return maxDepth;
    }
}
```

---

## 🧪 Another Example

```text
Input:
"(1+(2*3)+((8)/4))+1"
```

Maximum nesting:

```text
((8)/4)
```

Depth:

```text
(       → 1
((      → 2
(((     → 3
```

So:

```text
Output:
3
```

Another example:

```text
Input:
"1"

Output:
0
```

There are no parentheses, so the depth remains `0`.

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

Your code creates a `StringBuilder` and may store characters in it, although that content is **not needed for calculating the answer**.

The depth variables themselves use `O(1)` extra space.

---

## 📌 Key Takeaways

* `depth` represents the **current nesting level**.
* `(` increases depth.
* `)` decreases depth.
* `maxDepth` stores the deepest level reached.
* Update `maxDepth` immediately after increasing `depth`.

### 🧠 Pattern to Remember

```text
(
↓
depth++

update maximum

)
↓
depth--
```

**One observation:** `StringBuilder ans` is unnecessary for this problem because we only need the maximum depth, not the modified string. Your depth logic is the part that actually solves LC 1614.
