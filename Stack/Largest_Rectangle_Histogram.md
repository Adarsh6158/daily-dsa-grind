## 📌 Problem Statement

Given an array of integers `heights` representing the histogram's bar height where the width of each bar is `1`, return the area of the largest rectangle in the histogram.

Leetcode Link : https://leetcode.com/problems/largest-rectangle-in-histogram/

## Examples

### Example 1
- **Input:** `heights = [2,1,5,6,2,3]`
- **Output:** `10`

### Example 2
- **Input:** `heights = [2,4]`
- **Output:** `4`

## Constraints

- `1 <= heights.length <= 10^5`
- `0 <= heights[i] <= 10^4`

# Approaches

## 1. Brute Force

### Idea
- For each bar, expand left and right until smaller height found
- Calculate area

### Time Complexity
- `O(n^2)`

### Space Complexity
- `O(1)`

### Code (Java)
```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        int n = heights.length;
        int maxArea = 0;

        for (int i = 0; i < n; i++) {
            int height = heights[i];
            int left = i;
            int right = i;

            while (left >= 0 && heights[left] >= height) left--;
            while (right < n && heights[right] >= height) right++;

            int width = right - left - 1;
            maxArea = Math.max(maxArea, height * width);
        }

        return maxArea;
    }
}
```

## 2. Stack (Optimal)

### Idea

* Use stack to store indices
* Maintain increasing heights
* When smaller height comes, calculate area

### Time Complexity

* `O(n)`

### Space Complexity

* `O(n)`

### Code (Java)

```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        Stack<Integer> stack = new Stack<>();
        int maxArea = 0;
        int n = heights.length;

        for (int i = 0; i <= n; i++) {
            int h = (i == n) ? 0 : heights[i];

            while (!stack.isEmpty() && h < heights[stack.peek()]) {
                int height = heights[stack.pop()];
                int width = stack.isEmpty() ? i : i - stack.peek() - 1;
                maxArea = Math.max(maxArea, height * width);
            }

            stack.push(i);
        }

        return maxArea;
    }
}
```

## 3. Precompute Left and Right Boundaries

### Idea

* Find next smaller element to left and right
* Compute width using boundaries

### Time Complexity

* `O(n)`

### Space Complexity

* `O(n)`

### Code (Java)

```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        int n = heights.length;
        int[] left = new int[n];
        int[] right = new int[n];

        Stack<Integer> stack = new Stack<>();

        for (int i = 0; i < n; i++) {
            while (!stack.isEmpty() && heights[stack.peek()] >= heights[i]) {
                stack.pop();
            }
            left[i] = stack.isEmpty() ? -1 : stack.peek();
            stack.push(i);
        }

        stack.clear();

        for (int i = n - 1; i >= 0; i--) {
            while (!stack.isEmpty() && heights[stack.peek()] >= heights[i]) {
                stack.pop();
            }
            right[i] = stack.isEmpty() ? n : stack.peek();
            stack.push(i);
        }

        int maxArea = 0;
        for (int i = 0; i < n; i++) {
            int width = right[i] - left[i] - 1;
            maxArea = Math.max(maxArea, heights[i] * width);
        }

        return maxArea;
    }
}
```

## Visualization

```id="lrhviz1"
heights = [2,1,5,6,2,3]

Stack keeps increasing bars
When smaller bar comes → compute area
```

## Edge Cases

* Single bar
* All bars same height
* Increasing heights
* Decreasing heights
* Zero heights

## Why NOT Other Approaches

### Brute Force

```java id="lrhbf1"
expand left and right for each bar
```

* `O(n^2)` time
* Not scalable

## Follow-up Variations

### 1. Max rectangle in binary matrix

```java id="lrhvar1"
convert rows to histogram
```

### 2. Return rectangle indices

```java id="lrhvar2"
track left and right boundaries
```

## Conclusion

| Approach        | Time Complexity | Space Complexity | Notes       |
| --------------- | --------------- | ---------------- | ----------- |
| Brute Force     | O(n^2)          | O(1)             | Not usable  |
| Stack           | O(n)            | O(n)             | Optimal     |
| Boundary Arrays | O(n)            | O(n)             | Alternative |
