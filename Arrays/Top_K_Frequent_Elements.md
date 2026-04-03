## 📌 Problem Statement

Given an integer array `nums` and an integer `k`, return the `k` most frequent elements.

You may return the answer in any order.

Leetcode Link: [https://leetcode.com/problems/top-k-frequent-elements/](https://leetcode.com/problems/top-k-frequent-elements/)


## Examples

### Example 1

* **Input:** `nums = [1,1,1,2,2,3], k = 2`
* **Output:** `[1,2]`

### Explanation

* `1 → frequency = 3`
* `2 → frequency = 2`
* `3 → frequency = 1`
  Top 2 frequent → `[1,2]`


### Example 2

* **Input:** `nums = [1], k = 1`
* **Output:** `[1]`


## Constraints

* `1 <= nums.length <= 10^5`
* `-10^4 <= nums[i] <= 10^4`
* `k` is in the range `[1, number of unique elements]`


# Approaches


## 1. Sorting Based Approach

### Idea

* Count frequency using HashMap
* Sort elements based on frequency (descending)
* Pick top `k` elements


### Visualization

```id="viz1"
nums = [1,1,1,2,2,3]

Step 1: Frequency Map
1 → 3
2 → 2
3 → 1

Step 2: Sort by frequency ↓
[1, 2, 3]

Step 3: Pick k = 2
Result → [1,2]
```


### Time Complexity

* `O(n log n)`

### Space Complexity

* `O(n)`


### Code (Java)

```java
import java.util.*;

class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        HashMap<Integer, Integer> map = new HashMap<>();

        for (int num : nums) {
            map.put(num, map.getOrDefault(num, 0) + 1);
        }

        List<Integer> list = new ArrayList<>(map.keySet());

        list.sort((a, b) -> map.get(b) - map.get(a));

        int[] result = new int[k];
        for (int i = 0; i < k; i++) {
            result[i] = list.get(i);
        }

        return result;
    }
}
```


## 2. Min Heap (Optimal)

### Idea

* Use HashMap for frequency
* Use Min Heap of size `k`
* Keep only top `k` frequent elements


### Visualization

```id="viz2"
nums = [1,1,1,2,2,3], k = 2

Frequency Map:
1 → 3
2 → 2
3 → 1

Heap Process:
Add (1,3) → heap = [1]
Add (2,2) → heap = [2,1]
Add (3,1) → remove smallest → heap = [2,1]

Result → [1,2]
```
<img width="944" height="535" alt="image" src="https://github.com/user-attachments/assets/369ba3e4-8545-4f3f-aaa0-21ad5aa51eb6" />

---

### Time Complexity

* `O(n log k)`

### Space Complexity

* `O(n)`


### Code (Java)

```java
import java.util.*;

class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        HashMap<Integer, Integer> map = new HashMap<>();

        for (int num : nums) {
            map.put(num, map.getOrDefault(num, 0) + 1);
        }

        PriorityQueue<Integer> heap =
                new PriorityQueue<>((a, b) -> map.get(a) - map.get(b));

        for (int num : map.keySet()) {
            heap.add(num);
            if (heap.size() > k) {
                heap.poll();
            }
        }

        int[] result = new int[k];
        int i = 0;

        for (int num : heap) {
            result[i++] = num;
        }

        return result;
    }
}
```


## 3. Bucket Sort (Most Optimal)

### Idea

* Frequency max = `n`
* Create buckets where index = frequency
* Traverse from high frequency to low


### Visualization

```id="viz3"
nums = [1,1,1,2,2,3]

Frequency Map:
1 → 3
2 → 2
3 → 1

Buckets:
index 1 → [3]
index 2 → [2]
index 3 → [1]

Traverse from back:
[1,2]
```
<img width="1035" height="487" alt="image" src="https://github.com/user-attachments/assets/f07943fe-fc39-46f1-be28-2a694e8183a3" />



### Time Complexity

* `O(n)`

### Space Complexity

* `O(n)`


### Code (Java)

```java
import java.util.*;

class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        HashMap<Integer, Integer> map = new HashMap<>();

        for (int num : nums) {
            map.put(num, map.getOrDefault(num, 0) + 1);
        }

        List<Integer>[] bucket = new List[nums.length + 1];

        for (int key : map.keySet()) {
            int freq = map.get(key);

            if (bucket[freq] == null) {
                bucket[freq] = new ArrayList<>();
            }

            bucket[freq].add(key);
        }

        List<Integer> result = new ArrayList<>();

        for (int i = bucket.length - 1; i >= 0 && result.size() < k; i--) {
            if (bucket[i] != null) {
                result.addAll(bucket[i]);
            }
        }

        return result.stream().mapToInt(i -> i).toArray();
    }
}
```

# Conclusion

| Approach    | Time Complexity | Space Complexity | Notes              |
| ----------- | --------------- | ---------------- | ------------------ |
| Sorting     | O(n log n)      | O(n)             | Brute Force        |
| Min Heap    | O(n log k)      | O(n)             | Optimal            |
| Bucket Sort | O(n)            | O(n)             | Most optimal       |

