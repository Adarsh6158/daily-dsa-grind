## 📌 Problem Statement

Given an array of integers `temperatures` representing the daily temperatures, return an array `answer` such that `answer[i]` is the number of days you have to wait after the `i-th` day to get a warmer temperature. If there is no future day, keep `0`.

Leetcode Link : https://leetcode.com/problems/daily-temperatures/

## Examples

### Example 1
- **Input:** `temperatures = [73,74,75,71,69,72,76,73]`
- **Output:** `[1,1,4,2,1,1,0,0]`

### Example 2
- **Input:** `temperatures = [30,40,50,60]`
- **Output:** `[1,1,1,0]`

### Example 3
- **Input:** `temperatures = [30,60,90]`
- **Output:** `[1,1,0]`

## Constraints

- `1 <= temperatures.length <= 10^5`
- `30 <= temperatures[i] <= 100`

# Approaches

## 1. Brute Force

### Idea
- For each day, scan forward to find next warmer day

### Time Complexity
- `O(n^2)`

### Space Complexity
- `O(1)`

### Code (Java)
```java
class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        int n = temperatures.length;
        int[] result = new int[n];

        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                if (temperatures[j] > temperatures[i]) {
                    result[i] = j - i;
                    break;
                }
            }
        }

        return result;
    }
}
```

## 2. Stack (Optimal)

### Idea

* Use stack to store indices
* Maintain decreasing temperatures
* When a warmer temperature is found, resolve previous indices

### Time Complexity

* `O(n)`

### Space Complexity

* `O(n)`

### Code (Java)

```java
class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        int n = temperatures.length;
        int[] result = new int[n];
        Stack<Integer> stack = new Stack<>();

        for (int i = 0; i < n; i++) {
            while (!stack.isEmpty() && temperatures[i] > temperatures[stack.peek()]) {
                int prev = stack.pop();
                result[prev] = i - prev;
            }
            stack.push(i);
        }

        return result;
    }
}
```

## 3. Reverse Traversal (Optimized)

### Idea

* Traverse from right to left
* Jump using previously computed answers

### Time Complexity

* `O(n)`

### Space Complexity

* `O(1)`

### Code (Java)

```java
class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        int n = temperatures.length;
        int[] result = new int[n];

        for (int i = n - 2; i >= 0; i--) {
            int j = i + 1;

            while (j < n && temperatures[j] <= temperatures[i]) {
                if (result[j] == 0) {
                    j = n;
                } else {
                    j = j + result[j];
                }
            }

            if (j < n) {
                result[i] = j - i;
            }
        }

        return result;
    }
}
```

## Visualization

```id="dtviz1"
temperatures = [73,74,75,71,69,72,76,73]

Use stack:
Push indices
Pop when warmer day found
```

## Edge Cases

* Strictly decreasing temperatures → all `0`
* Strictly increasing temperatures
* All same temperatures
* Single element

## Why NOT Other Approaches

### Brute Force

```java
scan forward for each day
```

* `O(n^2)` time
* Not scalable

## Follow-up Variations

### 1. Previous warmer day

```java
reverse logic
```

### 2. Next smaller element

```java
change comparison
```

## Conclusion

| Approach          | Time Complexity | Space Complexity | Notes      |
| ----------------- | --------------- | ---------------- | ---------- |
| Brute Force       | O(n^2)          | O(1)             | Not usable |
| Stack             | O(n)            | O(n)             | Optimal    |
| Reverse Traversal | O(n)            | O(1)             | Optimized  |

