# Spiral Matrix

## 🔗 Problem Link

https://leetcode.com/problems/spiral-matrix/

## 🏷️ Tags

- Matrix
- Simulation

## 📚 Topics

- Array
- Matrix
- Simulation

## 📊 Difficulty

Medium

## 📖 Problem Statement

Given an `m × n` matrix, return all the elements of the matrix in **spiral order**.

---

## ✨ Examples

### Example 1

```text
Input:
[
 [1,2,3],
 [4,5,6],
 [7,8,9]
]

Output:
[1,2,3,6,9,8,7,4,5]
```

### Example 2

```text
Input:
[
 [1,2,3,4],
 [5,6,7,8],
 [9,10,11,12]
]

Output:
[1,2,3,4,8,12,11,10,9,5,6,7]
```

---

# 🚀 Approach

## Pattern Used

**Boundary Traversal (Simulation)**

---

## Intuition

Instead of moving randomly inside the matrix, keep four boundaries.

- Top
- Bottom
- Left
- Right

After traversing one side, move that boundary inward.

Repeat this until every element is visited.

---

## Understanding the Pattern

Imagine the matrix is surrounded by four walls.

```text
Top
────────────

Left        Right

────────────
Bottom
```

Initially,

```text
top = 0
bottom = rows - 1
left = 0
right = cols - 1
```

After every direction, one wall moves inside.

### Move Right

```text
Top Row

→ → →
```

After finishing,

```text
top++
```

---

### Move Down

```text
↓

↓

↓
```

After finishing,

```text
right--
```

---

### Move Left

```text
← ← ←
```

After finishing,

```text
bottom--
```

---

### Move Up

```text
↑

↑

↑
```

After finishing,

```text
left++
```

Then repeat the same process.

---

## Why This Approach Works

Every iteration completes one outer layer of the matrix.

After finishing a layer, the boundaries become smaller.

Eventually, all elements are visited exactly once.

---

## Algorithm

1. Initialize four boundaries.
2. Traverse from Left → Right.
3. Move the top boundary down.
4. Traverse from Top → Bottom.
5. Move the right boundary left.
6. Traverse from Right → Left.
7. Move the bottom boundary up.
8. Traverse from Bottom → Top.
9. Move the left boundary right.
10. Repeat until the boundaries cross.

---

## 💻 Java Solution

```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {

        int n = matrix.length;
        int m = matrix[0].length;

        int l = 0, r = m - 1;
        int t = 0, b = n - 1;

        List<Integer> list = new ArrayList<>();

        while (l <= r && t <= b) {

            // Right
            for (int i = l; i <= r; i++) {
                list.add(matrix[t][i]);
            }
            t++;

            // Down
            for (int i = t; i <= b; i++) {
                list.add(matrix[i][r]);
            }
            r--;

            // Left
            if (t <= b) {
                for (int i = r; i >= l; i--) {
                    list.add(matrix[b][i]);
                }
                b--;
            }

            // Up
            if (l <= r) {
                for (int i = b; i >= t; i--) {
                    list.add(matrix[i][l]);
                }
                l++;
            }
        }

        return list;
    }
}
```

---

# ⭐ Main Logic

### Four Boundaries

```java
int l = 0;
int r = m - 1;
int t = 0;
int b = n - 1;
```

These four variables decide which layer of the matrix we are currently traversing.

---

### Boundary Updates

```java
t++;
r--;
b--;
l++;
```

Every completed direction shrinks one boundary.

Without updating these boundaries, the traversal would never move to the inner layer.

> **Interview Takeaway**

Whenever you hear **Spiral Matrix**, immediately think of **4 Boundaries**.

```text
Top
Bottom
Left
Right
```

---

## 🧪 Dry Run

### Input

```text
1 2 3
4 5 6
7 8 9
```

Initial Boundaries

```text
Top = 0
Bottom = 2
Left = 0
Right = 2
```

---

### Move Right

```text
1 2 3
```

Output

```text
[1,2,3]
```

Update

```text
Top++
```

---

### Move Down

```text
6
9
```

Output

```text
[1,2,3,6,9]
```

Update

```text
Right--
```

---

### Move Left

```text
8 7
```

Output

```text
[1,2,3,6,9,8,7]
```

Update

```text
Bottom--
```

---

### Move Up

```text
4
```

Output

```text
[1,2,3,6,9,8,7,4]
```

Update

```text
Left++
```

---

Remaining Matrix

```text
5
```

Final Output

```text
[1,2,3,6,9,8,7,4,5]
```

---

## ⏱️ Complexity Analysis

### Time Complexity

**O(m × n)**

Every element is visited exactly once.

---

### Space Complexity

**O(1)** (Ignoring Output List)

Only four boundary variables are used.

The returned list is required by the problem.

---

## 📌 Constraints

- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= m, n <= 10`
- `-100 <= matrix[i][j] <= 100`

---

## 💡 Key Points

- Maintain four boundaries.
- Traverse in four directions.
- Shrink one boundary after every traversal.
- Continue until boundaries cross.
- Every element is visited exactly once.
- Check conditions before moving Left and Up.

---

## ⚠️ Common Mistakes

- Forgetting to update the boundaries.
- Missing the `if (t <= b)` condition.
- Missing the `if (l <= r)` condition.
- Traversing the same row or column twice.
- Infinite loop due to incorrect boundary updates.

---

## 📝 Revision Snapshot

**Problem Type:** Matrix Traversal

**Pattern Used:** Boundary Traversal (Simulation)

**Main Data Structure:** Matrix

**Boundaries**

```text
Top
Bottom
Left
Right
```

**Traversal Order**

```text
Right
↓

Down
↓

Left
↓

Up
```

**Boundary Updates**

```text
Top++

Right--

Bottom--

Left++
```

**Key Idea**

Traverse one complete outer layer.

Shrink the boundaries.

Repeat until all elements are visited.