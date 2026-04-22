## 📌 Problem Statement

Given an integer array `nums`, return all the triplets `[nums[i], nums[j], nums[k]]` such that:
- `i != j`, `i != k`, `j != k`
- `nums[i] + nums[j] + nums[k] == 0`

The solution set must not contain duplicate triplets.

Leetcode Link : https://leetcode.com/problems/3sum/

## Examples

### Example 1
- **Input:** `nums = [-1,0,1,2,-1,-4]`
- **Output:** `[[-1,-1,2],[-1,0,1]]`

### Example 2
- **Input:** `nums = [0,1,1]`
- **Output:** `[]`

### Example 3
- **Input:** `nums = [0,0,0]`
- **Output:** `[[0,0,0]]`

## Constraints

- `3 <= nums.length <= 3000`
- `-10^5 <= nums[i] <= 10^5`

# Approaches

## 1. Brute Force

### Idea
- Try all triplets `(i, j, k)`
- Check if sum is zero
- Use set to avoid duplicates

### Time Complexity
- `O(n^3)`

### Space Complexity
- `O(n)`

### Code (Java)
```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        Set<List<Integer>> set = new HashSet<>();
        int n = nums.length;

        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                for (int k = j + 1; k < n; k++) {
                    if (nums[i] + nums[j] + nums[k] == 0) {
                        List<Integer> temp = Arrays.asList(nums[i], nums[j], nums[k]);
                        Collections.sort(temp);
                        set.add(temp);
                    }
                }
            }
        }

        return new ArrayList<>(set);
    }
}
```

## 2. HashSet (Two Sum Based)

### Idea

* Fix one element
* Use set to find remaining two elements

### Time Complexity

* `O(n^2)`

### Space Complexity

* `O(n)`

### Code (Java)

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        Set<List<Integer>> result = new HashSet<>();
        int n = nums.length;

        for (int i = 0; i < n; i++) {
            Set<Integer> set = new HashSet<>();

            for (int j = i + 1; j < n; j++) {
                int target = -nums[i] - nums[j];

                if (set.contains(target)) {
                    List<Integer> temp = Arrays.asList(nums[i], nums[j], target);
                    Collections.sort(temp);
                    result.add(temp);
                }

                set.add(nums[j]);
            }
        }

        return new ArrayList<>(result);
    }
}
```

## 3. Sorting + Two Pointer (Optimal)

### Idea

* Sort the array
* Fix one element
* Use two pointers to find remaining two elements
* Skip duplicates

### Time Complexity

* `O(n^2)`

### Space Complexity

* `O(1)` (excluding output)

### Code (Java)

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> result = new ArrayList<>();
        int n = nums.length;

        for (int i = 0; i < n; i++) {

            if (i > 0 && nums[i] == nums[i - 1]) continue;

            int left = i + 1;
            int right = n - 1;

            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];

                if (sum == 0) {
                    result.add(Arrays.asList(nums[i], nums[left], nums[right]));
                    left++;
                    right--;

                    while (left < right && nums[left] == nums[left - 1]) left++;
                    while (left < right && nums[right] == nums[right + 1]) right--;

                } else if (sum < 0) {
                    left++;
                } else {
                    right--;
                }
            }
        }

        return result;
    }
}
```

## Visualization

```
nums = [-4,-1,-1,0,1,2]

Fix i = -1
left = -1, right = 2

-1 + -1 + 2 = 0
-1 + 0 + 1 = 0
```

## Edge Cases

* No valid triplet → return empty list
* All zeros → only one triplet `[0,0,0]`
* Duplicate numbers
* Large positive/negative values

## Why NOT Other Approaches

### Brute Force

```java
try all triplets
```

* `O(n^3)` time
* Not scalable

### HashSet Approach

```java
use set for two sum
```

* Extra space required
* Duplicate handling is complex

## Follow-up Variations

### 1. 3Sum Closest

```java
int target;
```

* Find triplet closest to target

### 2. 4Sum

```java
extend to 4 elements
```

* Add one more loop and apply two pointer

## Conclusion

| Approach    | Time Complexity | Space Complexity | Notes      |
| ----------- | --------------- | ---------------- | ---------- |
| Brute Force | O(n^3)          | O(n)             | Not usable |
| HashSet     | O(n^2)          | O(n)             | Medium     |
| Two Pointer | O(n^2)          | O(1)             | Optimal    |

