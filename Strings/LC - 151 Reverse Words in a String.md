**📁 Folder:** `Strings`

**File Name:** `LC - 151 Reverse Words in a String.md`

# 🧩 LeetCode 151 - Reverse Words in a String

## 🔗 Problem

[LeetCode - Reverse Words in a String](https://leetcode.com/problems/reverse-words-in-a-string/)

---

## 🏷️ Tags

* String
* StringBuilder

---

## 📚 Topics

* String Manipulation
* `split()`
* `trim()`
* StringBuilder
* Reverse Traversal

---

## 📊 Difficulty

Medium

---

## 💡 Intuition

We need to reverse the **order of words** in the string.

For example:

```text
Input:
"The sky is blue"

Output:
"blue is sky The"
```

We don't need to reverse the characters inside each word.

The easiest way is:

1. Remove leading/trailing spaces using `trim()`.
2. Split the string into words.
3. Traverse the words from **right to left**.
4. Build the answer using `StringBuilder`.

---

## 🧠 Thought Process

First, we need to handle multiple spaces.

For example:

```text
"  hello   world  "
```

Using:

```java
s.trim()
```

removes the spaces at the beginning and end.

Then:

```java
s.trim().split("\\s+")
```

splits the string wherever there is **one or more whitespace characters**.

So:

```text
"  hello   world  "
```

becomes:

```text
["hello", "world"]
```

Now we simply start from the last word.

```text
world → hello
```

and construct the result.

---

## 🔍 Dry Run

### Example

```text
s = "  the sky is blue  "
```

After:

```java
s.trim()
```

we get:

```text
"the sky is blue"
```

After:

```java
split("\\s+")
```

we get:

```text
["the", "sky", "is", "blue"]
```

Now traverse backwards:

```text
i = 3 → "blue"
i = 2 → "is"
i = 1 → "sky"
i = 0 → "the"
```

Build the answer:

```text
"blue is sky the"
```

---

## ⭐ Main Logic

The main part of the solution is:

```java
for(int i = words.length-1 ; i>= 0 ; i--){
```

We start from the **last word** and move towards the first.

### First word added

```java
if(ans.length()==0){
    ans.append(words[i]);
}
```

If `ans` is empty, we simply add the word.

Example:

```text
ans = ""
word = "blue"

ans = "blue"
```

### Remaining words

For the remaining words:

```java
else{
    ans.append(" " + words[i]);
}
```

We add a space before the word.

So:

```text
blue
blue + " " + is
blue is + " " + sky
blue is sky + " " + the
```

Final:

```text
"blue is sky the"
```

---

## 🎯 Key Pattern

### Extract → Reverse Traverse → Build

Whenever you need to reverse the **order of words**, think:

```text
String
  ↓
trim()
  ↓
split("\\s+")
  ↓
Traverse from right → left
  ↓
StringBuilder
```

Remember:

> We are reversing the **words**, not the characters.

---

## 💻 Java Solution

```java
class Solution {

    public String reverseWords(String s) {

        StringBuilder ans = new StringBuilder();

        String[] words = s.trim().split("\\s+");

        for(int i = words.length-1 ; i>= 0 ; i--){

            if(ans.length()==0){

                ans.append(words[i]);

            }else{

                ans.append(" " + words[i]);

            }

        }

        return ans.toString();

    }

}
```

---

## 🧪 Another Example

```text
Input:
"hello world"

Words:
["hello", "world"]

Reverse traversal:
world → hello

Output:
"world hello"
```

### With multiple spaces

```text
Input:
"a good   example"

After split:
["a", "good", "example"]

Reverse:
example → good → a

Output:
"example good a"
```

---

## ⏱️ Complexity

### Time Complexity

```text
O(n)
```

We process the string and all its words.

### Space Complexity

```text
O(n)
```

We store the words and the resulting string.

---

## 📌 Key Takeaways

* Use `trim()` to remove leading and trailing spaces.
* Use `split("\\s+")` to handle multiple spaces between words.
* Traverse the words from **right to left**.
* Use `StringBuilder` to construct the answer.
* `ans.length() == 0` helps decide whether a space is needed.

### 🧠 Pattern to Remember

```text
"the sky is blue"
        ↓
["the", "sky", "is", "blue"]
        ↓
Start from right
        ↓
"blue is sky the"
```
