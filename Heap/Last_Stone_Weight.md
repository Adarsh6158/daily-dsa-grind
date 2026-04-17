## 📌 Problem Statement

You are given an array of integers `stones` where `stones[i]` is the weight of the `i-th` stone.

We are playing a game with the stones. On each turn, we choose the two heaviest stones and smash them together.

* If both stones have the same weight, both are destroyed.
* If they have different weights, the smaller one is destroyed and the larger one becomes `x - y`.

Return the weight of the last remaining stone. If no stones remain, return `0`.

LeetCode Link: [https://leetcode.com/problems/last-stone-weight/](https://leetcode.com/problems/last-stone-weight/)


## Examples

### Example 1

* **Input:** `stones = [2,7,4,1,8,1]`
* **Output:** `1`


### Example 2

* **Input:** `stones = [1]`
* **Output:** `1`

## Constraints

* `1 <= stones.length <= 30`
* `1 <= stones[i] <= 1000`


# Approaches

## 1. Brute Force (Sorting Each Time)

### Idea

* Sort the array in descending order
* Take two largest elements
* Smash them and insert result back
* Repeat until one or zero stones remain

### Time Complexity

* `O(n^2 log n)`

### Space Complexity

* `O(1)`


### Code

```java id="bfstone"
import java.util.Arrays;

public class Solution {
    public int lastStoneWeight(int[] stones) {
        int n = stones.length;

        while (n > 1) {
            Arrays.sort(stones, 0, n);

            int y = stones[n - 1];
            int x = stones[n - 2];

            n -= 2;

            if (y != x) {
                stones[n] = y - x;
                n++;
            }
        }

        return n == 1 ? stones[0] : 0;
    }
}
```


## 2. Max Heap (Priority Queue) — Optimal

### Idea

* Use a max heap to always get the two largest stones
* Remove top two elements
* If not equal, insert their difference back
* Continue until one or zero stones remain


### Time Complexity

* `O(n log n)`

### Space Complexity

* `O(n)`


### Code

```java id="heapstone"
import java.util.PriorityQueue;
import java.util.Collections;

public class Solution {
    public int lastStoneWeight(int[] stones) {
        PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());

        for (int stone : stones) {
            maxHeap.add(stone);
        }

        while (maxHeap.size() > 1) {
            int y = maxHeap.poll();
            int x = maxHeap.poll();

            if (y != x) {
                maxHeap.add(y - x);
            }
        }

        return maxHeap.isEmpty() ? 0 : maxHeap.poll();
    }
}
```

## Conclusion

| Approach          | Time Complexity | Space Complexity | Notes            |
| ----------------- | --------------- | ---------------- | ---------------- |
| Sorting each time | O(n^2 log n)    | O(1)             | Inefficient      |
| Max Heap          | O(n log n)      | O(n)             | Optimal solution |
