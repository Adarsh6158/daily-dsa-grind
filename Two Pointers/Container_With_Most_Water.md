## 📌 Problem Statement

You are given an integer array `height` where `height[i]` represents the height of a vertical line at index `i`.

Find two lines that together with the x-axis form a container that holds the maximum amount of water.

Return the maximum amount of water a container can store.

Leetcode Link : https://leetcode.com/problems/container-with-most-water/

## Examples

### Example 1
- **Input:** `height = [1,8,6,2,5,4,8,3,7]`
- **Output:** `49`

### Example 2
- **Input:** `height = [1,1]`
- **Output:** `1`

## Constraints

- `2 <= height.length <= 10^5`
- `0 <= height[i] <= 10^4`

# Approaches

## 1. Brute Force

### Idea
- Try all pairs `(i, j)`
- Compute area = `min(height[i], height[j]) * (j - i)`

### Time Complexity
- `O(n^2)`

### Space Complexity
- `O(1)`

### Code (Java)
```java
class Solution {
    public int maxArea(int[] height) {
        int n = height.length;
        int maxArea = 0;

        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                int h = Math.min(height[i], height[j]);
                int w = j - i;
                maxArea = Math.max(maxArea, h * w);
            }
        }

        return maxArea;
    }
}
```

## 2. Two Pointer (Optimal)

### Idea

* Start with two pointers at both ends
* Calculate area
* Move the pointer with smaller height

### Time Complexity

* `O(n)`

### Space Complexity

* `O(1)`

### Code (Java)

```java
class Solution {
    public int maxArea(int[] height) {
        int left = 0;
        int right = height.length - 1;
        int maxArea = 0;

        while (left < right) {
            int h = Math.min(height[left], height[right]);
            int w = right - left;
            maxArea = Math.max(maxArea, h * w);

            if (height[left] < height[right]) {
                left++;
            } else {
                right--;
            }
        }

        return maxArea;
    }
}
```

## Visualization

```
height = [1,8,6,2,5,4,8,3,7]

left = 0, right = 8
area = min(1,7) * 8 = 8

move left

left = 1, right = 8
area = min(8,7) * 7 = 49
```

## Edge Cases

* Minimum size array `[x,y]`
* All heights are same
* Heights contain zero
* Increasing/decreasing heights

## Why NOT Other Approaches

### Brute Force

```java
try all pairs (i, j)
```

* `O(n^2)` time
* Not scalable for large input

## Follow-up Variations

### 1. Return indices of container

```java
int leftIndex, rightIndex;
```

* Track indices along with max area

### 2. Max area with at least k distance

```java
if (right - left >= k)
```

* Modify condition based on constraint

## Conclusion

| Approach    | Time Complexity | Space Complexity | Notes      |
| ----------- | --------------- | ---------------- | ---------- |
| Brute Force | O(n^2)          | O(1)             | Not usable |
| Two Pointer | O(n)            | O(1)             | Optimal    |

