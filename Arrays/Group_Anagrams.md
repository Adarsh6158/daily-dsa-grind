## 📌 Problem Statement  
Given an array of strings `strs`, group the **anagrams** together. You can return the answer in any order.

👉 Anagrams are words formed by rearranging letters of another word.

Leetcode Link: https://leetcode.com/problems/group-anagrams/

## Examples  

### Example 1  
- **Input:** `strs = ["eat","tea","tan","ate","nat","bat"]`  
- **Output:** `[["bat"],["nat","tan"],["ate","eat","tea"]]`  

### Explanation  
- `"nat"` & `"tan"` → same letters  
- `"ate","eat","tea"` → same letters  
- `"bat"` → no anagram  

### Example 2  
- **Input:** `strs = [""]`  
- **Output:** `[[""]]`  


### Example 3  
- **Input:** `strs = ["a"]`  
- **Output:** `[["a"]]`  


## Constraints  
- `1 <= strs.length <= 10^4`  
- `0 <= strs[i].length <= 100`  
- `strs[i]` consists of lowercase English letters  


# Approaches  


## 1. Sorting Based Approach  

### Idea  
- Sort each string  
- Use sorted string as key in HashMap  
- Group original strings  


### Visualization  

<img width="1006" height="482" alt="image" src="https://github.com/user-attachments/assets/94376297-33f7-49ff-bace-c87f50b6c31d" />

👉 Example:

``` id="viz1"
"eat" → "aet"
"tea" → "aet"
"ate" → "aet"

Same key → same group
````


### Time Complexity

* `O(n * k log k)`
  (k = length of each string)

### Space Complexity

* `O(n * k)`


### Code (Java)

```java
import java.util.*;

class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        HashMap<String, List<String>> map = new HashMap<>();

        for (String str : strs) {
            char[] arr = str.toCharArray();
            Arrays.sort(arr);

            String key = new String(arr);

            map.putIfAbsent(key, new ArrayList<>());
            map.get(key).add(str);
        }

        return new ArrayList<>(map.values());
    }
}
```

## 2. Frequency Count (Optimal)

### Idea

* Instead of sorting, count characters
* Build a key using frequency array
* Faster than sorting


### Visualization


👉 Example:

```id="viz2"
"eat" → count → [1a,1e,1t,...]
"tea" → same count → same key
```
<img width="1395" height="891" alt="group-anagrams-cover" src="https://github.com/user-attachments/assets/a6621452-c14c-47a3-9a33-7d0da372b5e1" />


### Time Complexity

* `O(n * k)`

### Space Complexity

* `O(n * k)`


### Code (Java)

```java id="optfreq"
import java.util.*;

class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        HashMap<String, List<String>> map = new HashMap<>();

        for (String str : strs) {
            int[] count = new int[26];

            for (char c : str.toCharArray()) {
                count[c - 'a']++;
            }

            String key = Arrays.toString(count);

            map.putIfAbsent(key, new ArrayList<>());
            map.get(key).add(str);
        }

        return new ArrayList<>(map.values());
    }
}
```


# Conclusion

| Approach        | Time Complexity | Space Complexity | Notes              |
| --------------- | --------------- | ---------------- | ------------------ |
| Sorting         | O(n * k log k)  | O(n * k)         | Brute Force        |
| Frequency Count | O(n * k)        | O(n * k)         | Optimal solution   |
