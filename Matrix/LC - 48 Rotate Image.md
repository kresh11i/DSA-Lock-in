# Rotate Image

## 🔗 Problem Link

https://leetcode.com/problems/rotate-image/

## 🏷️ Tags

- Matrix
- Array

## 📚 Topics

- Array
- Math
- Matrix

## 📊 Difficulty

Medium

## 📖 Problem Statement

You are given an `n × n` matrix representing an image.

Rotate the image by **90° clockwise**.

The rotation must be done **in-place**, meaning you cannot create another 2D matrix.

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
[
 [7,4,1],
 [8,5,2],
 [9,6,3]
]
```

### Example 2

```text
Input:
[
 [5,1,9,11],
 [2,4,8,10],
 [13,3,6,7],
 [15,14,12,16]
]

Output:
[
 [15,13,2,5],
 [14,3,4,1],
 [12,6,8,9],
 [16,7,10,11]
]
```

---

## 🚀 Approach

### Pattern Used

**Matrix Transformation (Transpose + Reverse)**

### Intuition

Rotating a matrix directly is difficult.

Instead, break the problem into **two simple operations**.

1. Transpose the matrix.
2. Reverse every row.

After these two operations, the matrix becomes rotated by **90° clockwise**.

---

### Why This Approach Works

A clockwise rotation can be achieved by changing the rows into columns first.

This is done using **Transpose**.

After transposing, every row is reversed to place the elements in their correct rotated positions.

Instead of moving every element individually, we use two simple operations that together produce the required rotation.

---

### Algorithm

1. Traverse only the upper half of the matrix.
2. Swap `matrix[i][j]` with `matrix[j][i]` to transpose the matrix.
3. Traverse every row.
4. Reverse each row using two pointers.
5. The matrix is now rotated by **90° clockwise**.

---

## 💻 Java Solution

```java
class Solution {
    public void rotate(int[][] matrix) {

        int n = matrix.length;

        // Transpose
        for (int i = 0; i < n; i++) {

            for (int j = i + 1; j < n; j++) {

                int temp1 = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp1;
            }
        }

        // Reverse every row
        for (int i = 0; i < n; i++) {

            int left = 0;
            int right = n - 1;

            while (left < right) {

                int temp2 = matrix[i][left];
                matrix[i][left] = matrix[i][right];
                matrix[i][right] = temp2;

                left++;
                right--;
            }
        }
    }
}
```

---

## ⭐ Main Logic

### Step 1 — Transpose the Matrix

```java
matrix[i][j] = matrix[j][i];
matrix[j][i] = temp1;
```

This converts every row into a column.

---

### Step 2 — Reverse Every Row

```java
matrix[i][left] = matrix[i][right];
matrix[i][right] = temp2;
```

Reversing each row completes the 90° clockwise rotation.

## 🔍 Understanding the Transpose

### What is Transpose?

Transpose means converting **rows into columns**.

For every element above the main diagonal, we swap it with its corresponding element below the diagonal.

Example:

Original Matrix

```text
1 2 3
4 5 6
7 8 9
```

After Transpose

```text
1 4 7
2 5 8
3 6 9
```

---

### Why do we start with `j = i + 1`?

```java
for (int i = 0; i < n; i++) {
    for (int j = i + 1; j < n; j++) {
        swap(matrix[i][j], matrix[j][i]);
    }
}
```

The main diagonal elements never change.

```text
★ = Main Diagonal

★ 2 3
4 ★ 6
7 8 ★
```

We only need to swap the elements **above the diagonal**.

---

### What happens if `j = 0`?

Suppose we have

```text
1 2
3 4
```

When `i = 0`

```text
Swap (0,1) ↔ (1,0)

1 3
2 4
```

Looks correct.

But when `i = 1`

```text
Swap (1,0) ↔ (0,1)
```

It swaps the same elements **again**.

```text
1 2
3 4
```

The transpose gets undone.

So every pair gets swapped **twice**, giving the original matrix back.

---

### Why `j = i + 1`?

Starting from

```java
j = i + 1;
```

means:

- Skip the main diagonal.
- Only visit the upper triangle.
- Every pair is swapped exactly **once**.
- No duplicate swaps.

---

### Visualization

```text
Matrix

★ X X
X ★ X
X X ★

Legend

★ = Ignore
X = Swap
```

We only traverse the highlighted upper half.

---

### Interview Takeaway

Whenever you write transpose:

```java
for (int i = 0; i < n; i++) {
    for (int j = i + 1; j < n; j++) {
        // swap
    }
}
```

Immediately remember:

- `i` → current row
- `j = i + 1` → start after the diagonal
- Every pair is swapped only once
- Prevents undoing previous swaps

> **Interview Takeaway:**  
> Whenever you are asked to rotate a matrix by **90° clockwise**, immediately think:

```text
Transpose
      ↓
Reverse Every Row
```

---

## 🧪 Dry Run

### Input

```text
[
 [1,2,3],
 [4,5,6],
 [7,8,9]
]
```

---

### Step 1 — Transpose

Swap across the diagonal.

```text
[
 [1,4,7],
 [2,5,8],
 [3,6,9]
]
```

---

### Step 2 — Reverse Every Row

Reverse each row individually.

```text
Row 1

[1,4,7]

↓

[7,4,1]
```

```text
Row 2

[2,5,8]

↓

[8,5,2]
```

```text
Row 3

[3,6,9]

↓

[9,6,3]
```

---

### Final Output

```text
[
 [7,4,1],
 [8,5,2],
 [9,6,3]
]
```

---

## ⏱️ Complexity Analysis

### Time Complexity

**O(n²)**

- Transpose → **O(n²)**
- Reverse every row → **O(n²)**

Overall Time Complexity = **O(n²)**

### Space Complexity

**O(1)**

- Rotation is performed in-place.

---

## 📌 Constraints

- `n == matrix.length`
- `n == matrix[i].length`
- `1 <= n <= 20`
- `-1000 <= matrix[i][j] <= 1000`

---

## 💡 Key Points

- Matrix must be rotated **in-place**.
- No extra 2D matrix is allowed.
- First transpose the matrix.
- Then reverse every row.
- Transpose changes rows into columns.
- Row reversal completes the clockwise rotation.

---

## ⚠️ Common Mistakes

- Reversing rows before transposing.
- Traversing the entire matrix during transpose.
- Swapping elements twice.
- Using `j = 0` instead of `j = i + 1`.
- Creating another 2D matrix unnecessarily.

---

## 📝 Revision Snapshot

**Problem Type:** Matrix Rotation

**Pattern Used:** Matrix Transformation (Transpose + Reverse)

**Main Data Structure:** Matrix

**Main Flow**

```text
Original Matrix
      │
      ▼
Transpose
      │
      ▼
Reverse Every Row
      │
      ▼
90° Clockwise Rotation
```

**Key Idea**

```text
Transpose
      +
Reverse Every Row
      =
90° Clockwise Rotation
```