## 📌 Problem Statement

Given two strings `s1` and `s2`, return `true` if `s2` contains a permutation of `s1`, or `false` otherwise.

In other words, return `true` if one of `s1`'s permutations is a substring of `s2`.

LeetCode Link: [https://leetcode.com/problems/permutation-in-string/](https://leetcode.com/problems/permutation-in-string/)

---

## Examples

### Example 1

* **Input:** `s1 = "ab", s2 = "eidbaooo"`
* **Output:** `true`
* **Explanation:** `s2` contains permutation `"ba"`

---

### Example 2

* **Input:** `s1 = "ab", s2 = "eidboaoo"`
* **Output:** `false`

---

## Constraints

* `1 <= s1.length, s2.length <= 10^4`
* `s1` and `s2` consist of lowercase English letters

---

# Approaches

## 1. Brute Force

### Idea

* Generate all permutations of `s1`
* Check if any permutation exists in `s2`

---

### Time Complexity

* `O(n! * m)`

### Space Complexity

* `O(n!)`

---

### Code (Java)

```java id="bfperm"
import java.util.*;

public class Solution {
    public boolean checkInclusion(String s1, String s2) {
        Set<String> set = new HashSet<>();
        permute("", s1, set);

        for (String str : set) {
            if (s2.contains(str)) {
                return true;
            }
        }
        return false;
    }

    private void permute(String prefix, String remaining, Set<String> set) {
        if (remaining.length() == 0) {
            set.add(prefix);
            return;
        }

        for (int i = 0; i < remaining.length(); i++) {
            permute(prefix + remaining.charAt(i),
                    remaining.substring(0, i) + remaining.substring(i + 1),
                    set);
        }
    }
}
```

---

## 2. Sliding Window with Sorting

### Idea

* Sort `s1`
* Check every substring of length `s1.length()` in `s2`
* Sort and compare

---

### Time Complexity

* `O(n * k log k)`

### Space Complexity

* `O(k)`

---

### Code (Java)

```java id="sortsw"
import java.util.Arrays;

public class Solution {
    public boolean checkInclusion(String s1, String s2) {
        char[] s1Arr = s1.toCharArray();
        Arrays.sort(s1Arr);
        String sortedS1 = new String(s1Arr);

        int k = s1.length();

        for (int i = 0; i <= s2.length() - k; i++) {
            char[] window = s2.substring(i, i + k).toCharArray();
            Arrays.sort(window);
            if (sortedS1.equals(new String(window))) {
                return true;
            }
        }

        return false;
    }
}
```

---

## 3. Sliding Window with Frequency Count (Optimal)

### Idea

* Use two frequency arrays of size 26
* Maintain a sliding window of size `s1.length()`
* Compare frequency arrays

---

### Time Complexity

* `O(n)`

### Space Complexity

* `O(1)`

---

### Code (Java)

```java id="optfreq"
public class Solution {
    public boolean checkInclusion(String s1, String s2) {
        if (s1.length() > s2.length()) return false;

        int[] s1Count = new int[26];
        int[] windowCount = new int[26];

        for (char c : s1.toCharArray()) {
            s1Count[c - 'a']++;
        }

        int k = s1.length();

        for (int i = 0; i < s2.length(); i++) {
            windowCount[s2.charAt(i) - 'a']++;

            if (i >= k) {
                windowCount[s2.charAt(i - k) - 'a']--;
            }

            if (matches(s1Count, windowCount)) {
                return true;
            }
        }

        return false;
    }

    private boolean matches(int[] a, int[] b) {
        for (int i = 0; i < 26; i++) {
            if (a[i] != b[i]) return false;
        }
        return true;
    }
}
```

---

## Conclusion

| Approach                         | Time Complexity | Space Complexity | Notes         |
| -------------------------------- | --------------- | ---------------- | ------------- |
| Brute Force                      | O(n! * m)       | O(n!)            | Not practical |
| Sliding Window + Sorting         | O(n * k log k)  | O(k)             | Better        |
| Sliding Window + Frequency Count | O(n)            | O(1)             | Optimal       |
