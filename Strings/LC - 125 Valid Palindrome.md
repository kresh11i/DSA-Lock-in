**📁 Folder:** `Strings`

**File Name:** `LC - 125 Valid Palindrome.md`

# 🧩 Valid Palindrome

## 🔗 Problem

[LeetCode 125 — Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)

---

## 🏷️ Tags

`String` `Two Pointer` `Palindrome`

## 📚 Topics

* String processing
* Character validation
* Two Pointers
* Palindrome

## 📊 Difficulty

**Easy**

---

## 💡 Intuition

The string may contain:

* Uppercase letters
* Lowercase letters
* Numbers
* Spaces
* Special characters

For this problem, we only care about **letters and digits**.

So my approach is:

1. Convert the string to lowercase.
2. Remove everything except letters and digits.
3. Use two pointers:

   * `left` from the beginning
   * `right` from the end
4. Compare both characters.
5. If they are different → `false`.
6. If all characters match → `true`.

For example:

```text
"A man, a plan, a canal: Panama"
```

After removing spaces/special characters and converting to lowercase:

```text
"amanaplanacanalpanama"
```

This is a palindrome.

---

## 🧠 Thought Process

### Step 1 — Convert to lowercase

```java
String lowerCase = s.toLowerCase();
```

This makes the comparison case-insensitive.

For example:

```text
"A" → "a"
```

---

### Step 2 — Keep only letters and digits

```java
if (Character.isLetterOrDigit(lowerCase.charAt(i))) {
    ans.append(lowerCase.charAt(i));
}
```

So characters like:

```text
' '
','
':'
'!'
```

are ignored.

The cleaned string is stored in:

```java
StringBuilder ans
```

---

### Step 3 — Use two pointers

```java
int left = 0, right = ans.length() - 1;
```

We start from both ends:

```text
left →              ← right
a m a n a p l a n a
```

Then:

```java
while (left < right)
```

compare:

```java
ans.charAt(left)
ans.charAt(right)
```

If they don't match:

```java
return false;
```

Otherwise:

```java
left++;
right--;
```

and continue moving toward the center.

---

## 🔍 Dry Run

### Input

```text
"A man, a plan, a canal: Panama"
```

### After lowercase

```text
"a man, a plan, a canal: panama"
```

### After removing non-alphanumeric characters

```text
"amanaplanacanalpanama"
```

Now:

```text
left → a m a n a p l a n a ... a n a l p a n a m a ← right
```

Compare:

```text
a == a ✅
m == m ✅
a == a ✅
n == n ✅
...
```

Continue until:

```text
left >= right
```

No mismatch was found.

Therefore:

```text
true
```

---

## ⭐ Main Logic

The important part is the two-pointer comparison:

```java
while (left < right) {
    if (ans.charAt(left) != ans.charAt(right)) {
        return false;
    } else {
        left++;
        right--;
    }
}
```

Think of it as:

```text
Start from both ends
        ↓
Compare
        ↓
Different? → false
        ↓
Same? → move both pointers
        ↓
Reach middle → true
```

---

## 🎯 Key Pattern

### Two Pointers — Opposite Direction

```text
left →              ← right

Compare both
   ↓
Move inward
   ↓
Repeat
```

This is a very common pattern for palindrome problems.

---

## 💻 Java Solution

```java
class Solution {
    public boolean isPalindrome(String s) {
        StringBuilder ans = new StringBuilder();
        String lowerCase = s.toLowerCase();

        for (int i = 0; i < s.length(); i++) {

            if (Character.isLetterOrDigit(lowerCase.charAt(i))) {
                ans.append(lowerCase.charAt(i));
            }
        }

        int left = 0, right = ans.length() - 1;

        while (left < right) {
            if (ans.charAt(left) != ans.charAt(right)) {
                return false;
            } else {
                left++;
                right--;
            }
        }

        return true;
    }
}
```

---

## 🧪 Another Example

### Input

```text
"race a car"
```

Cleaned string:

```text
"raceacar"
```

Compare:

```text
r == r ✅
a == a ✅
c != a ❌
```

Immediately:

```text
false
```

---

## ⏱️ Complexity

### Time — `O(n)`

We traverse the string to clean it and then traverse the cleaned string with two pointers.

Overall:

```text
O(n)
```

### Space — `O(n)`

`StringBuilder` stores the cleaned version of the string.

---

## 📌 Key Takeaways

* First normalize the string by converting it to lowercase.
* Ignore non-alphanumeric characters.
* Store the valid characters in `StringBuilder`.
* Use **two pointers from opposite ends**.
* Compare characters and move inward.
* A mismatch immediately means it is not a palindrome.
* Pattern: **String Cleaning + Two Pointers**.
