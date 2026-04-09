## 📌 Problem Statement
You are climbing a staircase. It takes `n` steps to reach the top.

Each time you can either climb:
- **1 step**
- **2 steps**

👉 Return the number of distinct ways to reach the top.

🔗 Leetcode Link: https://leetcode.com/problems/climbing-stairs/

```

n = 1 → 1 way  → [1]

n = 2 → 2 ways → [1+1], [2]

n = 3 → 3 ways →
[1+1+1], [1+2], [2+1]

```

---

### Recurrence Relation
👉 To reach step `n`:
```

f(n) = f(n-1) + f(n-2)

````

- From `n-1` → take 1 step  
- From `n-2` → take 2 steps  

---

## Examples

### Example 1
- **Input:** `n = 2`
- **Output:** `2`

### Example 2
- **Input:** `n = 3`
- **Output:** `3`

---

## Constraints
- `1 <= n <= 45`


## 1️⃣ Recursion (Brute Force)

### Idea
- Try all possible ways (1 step or 2 steps)
- Leads to repeated calculations

### Time Complexity
- `O(2^n)`

### Space Complexity
- `O(n)` (recursion stack)

### Code (Java)
```java
class Solution {
    public int climbStairs(int n) {
        if (n <= 2) return n;

        return climbStairs(n - 1) + climbStairs(n - 2);
    }
}
````

---

## 2️⃣ Dynamic Programming (Tabulation)

### Idea

* Store results to avoid recomputation
* Build solution from bottom-up

### Time Complexity

* `O(n)`

### Space Complexity

* `O(n)`

### Code (Java)

```java
class Solution {
    public int climbStairs(int n) {
        if (n <= 2) return n;

        int[] dp = new int[n + 1];
        dp[1] = 1;
        dp[2] = 2;

        for (int i = 3; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }

        return dp[n];
    }
}
```


## 3️⃣ Space Optimized (Best Approach)

### Idea

* Only last two values are needed
* Similar to Fibonacci

### Time Complexity

* `O(n)`

### Space Complexity

* `O(1)`

### Code (Java)

```java
class Solution {
    public int climbStairs(int n) {
        if (n <= 2) return n;

        int prev2 = 1;
        int prev1 = 2;

        for (int i = 3; i <= n; i++) {
            int curr = prev1 + prev2;
            prev2 = prev1;
            prev1 = curr;
        }

        return prev1;
    }
}
```


## DP Table Example

```
n:   1  2  3  4  5
dp:  1  2  3  5  8
```

## 🏁 Conclusion

| Approach        | Time Complexity | Space Complexity | Notes            |
| --------------- | --------------- | ---------------- | ---------------- |
| Recursion       | O(2^n)          | O(n)             | Not efficient    |
| DP (Tabulation) | O(n)            | O(n)             | Better           |
| Optimized       | O(n)            | O(1)             | Optimal          |


