## 📌 Problem Statement
Given an integer array `nums`, return `true` if any value appears **at least twice** in the array, and return `false` if every element is **distinct**.

Leetcode Link : https://leetcode.com/problems/contains-duplicate/description/

---

##  Examples

### Example 1
- **Input:** `nums = [1,2,3,1]`
- **Output:** `true`
- **Explanation:** The element `1` appears twice (index 0 and 3)

### Example 2
- **Input:** `nums = [1,2,3,4]`
- **Output:** `false`
- **Explanation:** All elements are distinct

### Example 3
- **Input:** `nums = [1,1,1,3,3,4,3,2,4,2]`
- **Output:** `true`

---

## Constraints
- `1 <= nums.length <= 10^5`
- `-10^9 <= nums[i] <= 10^9`

---

# Approaches

---

## 1. Brute Force Approach

### Idea
- Compare every element with every other element

### ⏱ Time Complexity
- `O(n^2)`

### Space Complexity
- `O(1)`

### Code (Java)
```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        for (int i = 0; i < nums.length; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[i] == nums[j]) {
                    return true;
                }
            }
        }
        return false;
    }
}
```

### 2. Sorting

Idea

Sort the array
Compare adjacent elements

Time Complexity  
O(n log n)

Space Complexity  
O(1) (ignoring sorting space)

Code

```java
import java.util.Arrays;

class Solution {
    public boolean containsDuplicate(int[] nums) {
        Arrays.sort(nums);

        for (int i = 1; i < nums.length; i++) {
            if (nums[i] == nums[i - 1]) {
                return true;
            }
        }
        return false;
    }
}
```

### 3. HashSet (Optimal)

Idea

Use a HashSet to track seen elements
If an element already exists, return true

Time Complexity  
O(n)

Space Complexity  
O(n)

Code

```java
import java.util.HashSet;

class Solution {
    public boolean containsDuplicate(int[] nums) {
        HashSet<Integer> set = new HashSet<>();

        for (int num : nums) {
            if (set.contains(num)) {
                return true;
            }
            set.add(num);
        }

        return false;
    }
}
```

## Conclusion

| Approach     | Time Complexity | Space Complexity | Notes                  |
|--------------|---------------|------------------|------------------------|
| Brute Force  | O(n²)         | O(1)             | Not efficient          |
| Sorting      | O(n log n)    | O(1)             | Better but not optimal |
| HashSet      | O(n)          | O(n)             | Best approach          |