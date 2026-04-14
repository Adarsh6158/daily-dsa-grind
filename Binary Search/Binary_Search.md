## 📌 Problem Statement

Given an array of distinct integers `nums`, sorted in ascending order, and an integer `target`, return the index of `target` if it exists in the array. Otherwise, return `-1`.

Your solution must run in `O(log n)` time.

LeetCode Link: [https://leetcode.com/problems/binary-search/](https://leetcode.com/problems/binary-search/)


## Examples

### Example 1

* **Input:** `nums = [-1,0,3,5,9,12], target = 9`
* **Output:** `4`
* **Explanation:** `9` exists at index 4


### Example 2

* **Input:** `nums = [-1,0,3,5,9,12], target = 2`
* **Output:** `-1`
* **Explanation:** `2` does not exist in the array


## Constraints

* `1 <= nums.length <= 10^4`
* `-10^4 < nums[i], target < 10^4`
* All integers in `nums` are unique
* `nums` is sorted in ascending order


# Approaches

## 1. Iterative Binary Search (Optimal)

### Idea

* Use two pointers `low` and `high`
* Find middle index
* If target found, return index
* If target is smaller, move left
* If target is greater, move right


### Time Complexity

* `O(log n)`

### Space Complexity

* `O(1)`


### Code (Java)

```java id="b1n4ry"
public class Solution {
    public int search(int[] nums, int target) {
        int low = 0;
        int high = nums.length - 1;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] < target) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }

        return -1;
    }
}
```


## 2. Recursive Binary Search

### Idea

* Divide the array recursively
* Check middle element
* Search left or right half accordingly


### Time Complexity

* `O(log n)`

### Space Complexity

* `O(log n)`


### Code (Java)

```java id="rec12"
public class Solution {
    public int search(int[] nums, int target) {
        return binarySearch(nums, target, 0, nums.length - 1);
    }

    private int binarySearch(int[] nums, int target, int low, int high) {
        if (low > high) return -1;

        int mid = low + (high - low) / 2;

        if (nums[mid] == target) return mid;
        else if (nums[mid] < target) return binarySearch(nums, target, mid + 1, high);
        else return binarySearch(nums, target, low, mid - 1);
    }
}
```

## Conclusion

| Approach  | Time Complexity | Space Complexity | Notes                   |
| --------- | --------------- | ---------------- | ----------------------- |
| Iterative | O(log n)        | O(1)             | Preferred in interviews |
| Recursive | O(log n)        | O(log n)         | Uses call stack         |
