# 📌 Majority Element

## 🧾 Problem Statement
Given an integer array `nums` of size `n`, return the **majority element**.

The majority element is the element that appears **more than ⌊n / 2⌋ times**.  
You may assume that the majority element **always exists**.

🔗 Leetcode Link: https://leetcode.com/problems/majority-element/


## 📘 Examples

### Example 1
- **Input:** `nums = [3,2,3]`
- **Output:** `3`

### Example 2
- **Input:** `nums = [2,2,1,1,1,2,2]`
- **Output:** `2`


## Constraints
- `n == nums.length`
- `1 <= n <= 5 * 10^4`
- `-10^9 <= nums[i] <= 10^9`


#  Approaches

## 1️⃣ Brute Force Approach

### Idea
- Count frequency of each element using nested loops
- If any element appears more than `n/2`, return it

### Time Complexity
- `O(n^2)`

### Space Complexity
- `O(1)`

### Code (Java)
```java
class Solution {
    public int majorityElement(int[] nums) {
        int n = nums.length;

        for (int i = 0; i < n; i++) {
            int count = 0;

            for (int j = 0; j < n; j++) {
                if (nums[i] == nums[j]) {
                    count++;
                }
            }

            if (count > n / 2) {
                return nums[i];
            }
        }

        return -1;
    }
}
````

## 2️⃣ HashMap Approach

### Idea

* Store frequency of elements using HashMap
* Return element whose frequency > `n/2`

### Time Complexity

* `O(n)`

### Space Complexity

* `O(n)`

### Code (Java)

```java
import java.util.HashMap;

class Solution {
    public int majorityElement(int[] nums) {
        HashMap<Integer, Integer> map = new HashMap<>();
        int n = nums.length;

        for (int num : nums) {
            map.put(num, map.getOrDefault(num, 0) + 1);

            if (map.get(num) > n / 2) {
                return num;
            }
        }

        return -1;
    }
}
```


## 3️⃣ Sorting Approach

### Idea

* Sort the array
* The majority element will always be at index `n/2`

### Time Complexity

* `O(n log n)`

### Space Complexity

* `O(1)` (ignoring sorting space)

### Code (Java)

```java
import java.util.Arrays;

class Solution {
    public int majorityElement(int[] nums) {
        Arrays.sort(nums);
        return nums[nums.length / 2];
    }
}
```


## 4️⃣ Boyer-Moore Voting Algorithm (Optimal)

### Idea

* Maintain:

  * `candidate`
  * `count`
* If count becomes 0 → change candidate
* If same → increment count
* Else → decrement count

👉 Majority element survives cancellation

### Time Complexity

* `O(n)`

### Space Complexity

* `O(1)`

### Code (Java)

```java
class Solution {
    public int majorityElement(int[] nums) {
        int candidate = 0;
        int count = 0;

        for (int num : nums) {
            if (count == 0) {
                candidate = num;
            }

            if (num == candidate) {
                count++;
            } else {
                count--;
            }
        }

        return candidate;
    }
}
```

## 🏁 Conclusion

| Approach    | Time Complexity | Space Complexity | Notes                        |
| ----------- | --------------- | ---------------- | ---------------------------- |
| Brute Force | O(n²)           | O(1)             | Not efficient                |
| HashMap     | O(n)            | O(n)             | Easy to implement            |
| Sorting     | O(n log n)      | O(1)             | Trick-based                  |
| Boyer-Moore | O(n)            | O(1)             | Optimal                      |


