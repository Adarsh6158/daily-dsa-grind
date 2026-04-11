## 📌 Problem Statement

Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['`, and `']'`, determine if the input string is valid.

A string is valid if:

* Open brackets are closed by the same type of brackets
* Open brackets are closed in the correct order
* Every close bracket has a corresponding open bracket

Leetcode Link: [https://leetcode.com/problems/valid-parentheses/](https://leetcode.com/problems/valid-parentheses/)

## Examples

### Example 1

* **Input:** `s = "()"`
* **Output:** `true`
* **Explanation:** Properly matched pair

### Example 2

* **Input:** `s = "()[]{}"`
* **Output:** `true`

### Example 3

* **Input:** `s = "(]"`
* **Output:** `false`

### Example 4

* **Input:** `s = "([)]"`
* **Output:** `false`

### Example 5

* **Input:** `s = "{[]}"`
* **Output:** `true`


## Constraints

* `1 <= s.length <= 10^4`
* `s` consists of parentheses only `'()[]{}'`


# Approaches

## 1. Brute Force Approach (Repeated Replacement)

### Idea

* Keep removing valid pairs `"()"`, `"{}"`, `"[]"` from string
* If string becomes empty → valid
* Otherwise → invalid

### Time Complexity

* `O(n^2)`

### Space Complexity

* `O(n)`

### Code (Java)

```java
class Solution {
    public boolean isValid(String s) {
        while (s.contains("()") || s.contains("{}") || s.contains("[]")) {
            s = s.replace("()", "")
                 .replace("{}", "")
                 .replace("[]", "");
        }
        return s.isEmpty();
    }
}
```


## 2. Stack Approach (Optimal)

### Idea

* Use a stack to track opening brackets
* When closing bracket appears:

  * Check if it matches top of stack
* If mismatch → invalid
* If stack empty at end → valid


### Time Complexity

* `O(n)`

### Space Complexity

* `O(n)`

<img width="993" height="478" alt="Screenshot 2026-04-11 at 3 44 47 PM" src="https://github.com/user-attachments/assets/f119da21-bec3-4000-8f5d-ce8509983cbd" />


### Code (Java)

```java
import java.util.Stack;

class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();

        for (char c : s.toCharArray()) {
            if (c == '(' || c == '{' || c == '[') {
                stack.push(c);
            } else {
                if (stack.isEmpty()) return false;

                char top = stack.pop();

                if ((c == ')' && top != '(') ||
                    (c == '}' && top != '{') ||
                    (c == ']' && top != '[')) {
                    return false;
                }
            }
        }

        return stack.isEmpty();
    }
}
```

## 3. Optimized Stack Using HashMap

### Idea

* Use `HashMap` for cleaner matching
* Reduces multiple condition checks


### Time Complexity

* `O(n)`

### Space Complexity

* `O(n)`


### Code (Java)

```java
import java.util.*;

class Solution {
    public boolean isValid(String s) {
        Map<Character, Character> map = new HashMap<>();
        map.put(')', '(');
        map.put('}', '{');
        map.put(']', '[');

        Stack<Character> stack = new Stack<>();

        for (char c : s.toCharArray()) {
            if (!map.containsKey(c)) {
                stack.push(c);
            } else {
                if (stack.isEmpty() || stack.pop() != map.get(c)) {
                    return false;
                }
            }
        }

        return stack.isEmpty();
    }
}
```

## Conclusion

| Approach        | Time Complexity | Space Complexity | Notes                    |
| --------------- | --------------- | ---------------- | ------------------------ |
| Brute Force     | O(n²)           | O(n)             | Not efficient            |
| Stack           | O(n)            | O(n)             | Standard                 |
| HashMap + Stack | O(n)            | O(n)             | Optimal                  |
