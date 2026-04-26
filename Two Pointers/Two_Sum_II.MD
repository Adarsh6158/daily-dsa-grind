## 📌 Problem Statement

Given a **1-indexed** array of integers `numbers` that is sorted in non-decreasing order, find two numbers such that they add up to a specific `target`.

Return the indices of the two numbers (1-indexed) as an array `[index1, index2]`.

You must use only constant extra space.

Leetcode Link : https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/

## Examples

### Example 1
- **Input:** `numbers = [2,7,11,15], target = 9`
- **Output:** `[1,2]`

### Example 2
- **Input:** `numbers = [2,3,4], target = 6`
- **Output:** `[1,3]`

### Example 3
- **Input:** `numbers = [-1,0], target = -1`
- **Output:** `[1,2]`

## Constraints

- `2 <= numbers.length <= 3 * 10^4`
- `-1000 <= numbers[i] <= 1000`
- `numbers` is sorted in non-decreasing order
- Exactly one solution exists

# Approaches

## 1. Brute Force

### Idea
- Try all pairs `(i, j)`
- Check if sum equals target

### Time Complexity
- `O(n^2)`

### Space Complexity
- `O(1)`

### Code (Java)
```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int n = numbers.length;

        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                if (numbers[i] + numbers[j] == target) {
                    return new int[]{i + 1, j + 1};
                }
            }
        }

        return new int[]{-1, -1};
    }
}
```

## 2. Binary Search

### Idea

* Fix one element
* Search for `target - numbers[i]` using binary search

### Time Complexity

* `O(n log n)`

### Space Complexity

* `O(1)`

### Code (Java)

```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int n = numbers.length;

        for (int i = 0; i < n; i++) {
            int left = i + 1;
            int right = n - 1;
            int required = target - numbers[i];

            while (left <= right) {
                int mid = left + (right - left) / 2;

                if (numbers[mid] == required) {
                    return new int[]{i + 1, mid + 1};
                } else if (numbers[mid] < required) {
                    left = mid + 1;
                } else {
                    right = mid - 1;
                }
            }
        }

        return new int[]{-1, -1};
    }
}
```

## 3. Two Pointer (Optimal)

### Idea

* Use two pointers at start and end
* Move pointers based on sum comparison

### Time Complexity

* `O(n)`

### Space Complexity

* `O(1)`

### Code (Java)

```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int left = 0;
        int right = numbers.length - 1;

        while (left < right) {
            int sum = numbers[left] + numbers[right];

            if (sum == target) {
                return new int[]{left + 1, right + 1};
            } else if (sum < target) {
                left++;
            } else {
                right--;
            }
        }

        return new int[]{-1, -1};
    }
}
```

## Visualization

```id="vizt2s"
numbers = [2,7,11,15], target = 9

left = 0 (2), right = 3 (15) → sum = 17 > 9 → move right
left = 0 (2), right = 2 (11) → sum = 13 > 9 → move right
left = 0 (2), right = 1 (7) → sum = 9 → answer
```

## Edge Cases

* Negative numbers
* Minimum size array
* Target formed by first and last element
* Duplicate values

## Why NOT Other Approaches

### Brute Force

```java id="bf2sum"
try all pairs
```

* `O(n^2)` time
* Not efficient

### HashMap

```java id="hm2sum"
use map to store values
```

* Uses extra space `O(n)`
* Not needed since array is sorted

## Follow-up Variations

### 1. Return values instead of indices

```java
return new int[]{numbers[left], numbers[right]};
```

### 2. Multiple solutions

```java
store all valid pairs
```

## Conclusion

| Approach      | Time Complexity | Space Complexity | Notes      |
| ------------- | --------------- | ---------------- | ---------- |
| Brute Force   | O(n^2)          | O(1)             | Not usable |
| Binary Search | O(n log n)      | O(1)             | Better     |
| Two Pointer   | O(n)            | O(1)             | Optimal    |
