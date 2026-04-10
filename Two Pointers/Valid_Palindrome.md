## 📌 Problem Statement

A phrase is a palindrome if, after:
- Converting all uppercase letters into lowercase  
- Removing all non-alphanumeric characters  

…it reads the same forward and backward.

Return `true` if the string is a palindrome, otherwise `false`.

Leetcode Link : https://leetcode.com/problems/valid-palindrome/description/


## Examples

### Example 1
- **Input:** `s = "A man, a plan, a canal: Panama"`
- **Output:** `true`
- **Explanation:** After cleaning → `"amanaplanacanalpanama"` which is a palindrome

### Example 2
- **Input:** `s = "race a car"`
- **Output:** `false`
- **Explanation:** After cleaning → `"raceacar"` which is not a palindrome

---

## Constraints

- `1 <= s.length <= 2 * 10^5`
- `s` consists only of printable ASCII characters


# Approaches

## 1. Brute Force (Clean + Reverse)

### Idea
- Remove non-alphanumeric characters
- Convert to lowercase
- Reverse string and compare

### Time Complexity
- `O(n)`

### Space Complexity
- `O(n)`

### Code (Java)
```java
class Solution {
    public boolean isPalindrome(String s) {
        StringBuilder clean = new StringBuilder();

        for (char c : s.toCharArray()) {
            if (Character.isLetterOrDigit(c)) {
                clean.append(Character.toLowerCase(c));
            }
        }

        String str = clean.toString();
        String rev = clean.reverse().toString();

        return str.equals(rev);
    }
}
````


## 2. Two Pointer (Optimal)

### Idea

* Use two pointers (`left`, `right`)
* Skip non-alphanumeric characters
* Compare characters ignoring case

### Time Complexity

* `O(n)`

### Space Complexity

* `O(1)`

### Code (Java)

```java
class Solution {
    public boolean isPalindrome(String s) {
        int left = 0;
        int right = s.length() - 1;

        while (left < right) {

            while (left < right && !Character.isLetterOrDigit(s.charAt(left))) {
                left++;
            }

            while (left < right && !Character.isLetterOrDigit(s.charAt(right))) {
                right--;
            }

            if (Character.toLowerCase(s.charAt(left)) != 
                Character.toLowerCase(s.charAt(right))) {
                return false;
            }

            left++;
            right--;
        }

        return true;
    }
}
```

## Visualization

### Step 1: Cleaning the String

```
"A man, a plan, a canal: Panama"
↓
"amanaplanacanalpanama"
```

### Step 2: Two Pointer Check

```
left → ← right
a m a n a p l a n a c a n a l p a n a m a
✔ ✔ ✔ ✔ ✔ ✔ ✔ ✔ ✔ ✔ ✔ ✔ ✔ ✔ ✔ ✔ ✔ ✔ ✔ ✔
```

## Conclusion

| Approach        | Time Complexity | Space Complexity | Notes              |
| --------------- | --------------- | ---------------- | ------------------ |
| Clean + Reverse | O(n)            | O(n)             | Easy               |
| Two Pointer     | O(n)            | O(1)             | Optimal            |
