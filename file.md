# Minimum Index of a Valid Split

## Problem Statement
An element `x` of an integer array `arr` of length `m` is **dominant** if more than half the elements of `arr` have a value of `x`.

You are given a **0-indexed** integer array `nums` of length `n` with one dominant element.

You can split `nums` at an index `i` into two arrays `nums[0, ..., i]` and `nums[i + 1, ..., n - 1]`, but the split is only valid if:
- `0 <= i < n - 1`
- `nums[0, ..., i]` and `nums[i + 1, ..., n - 1]` have the same dominant element.

Return the **minimum index** of a valid split. If no valid split exists, return `-1`.

## Example
### Example 1:
**Input:**
```plaintext
nums = [1,2,2,2]
```
**Output:**
```plaintext
2
```
**Explanation:**
We can split the array at index `2` to obtain arrays `[1,2,2]` and `[2]`. The dominant element is `2` in both subarrays.

### Example 2:
**Input:**
```plaintext
nums = [2,1,3,1,1,1,7,1,2,1]
```
**Output:**
```plaintext
4
```
**Explanation:**
We can split the array at index `4` to obtain arrays `[2,1,3,1,1]` and `[1,7,1,2,1]`. The dominant element is `1` in both subarrays.

### Example 3:
**Input:**
```plaintext
nums = [3,3,3,3,7,2,2]
```
**Output:**
```plaintext
-1
```
**Explanation:**
No valid split exists.

## Constraints
- `1 <= nums.length <= 10^5`
- `1 <= nums[i] <= 10^9`
- `nums` has exactly **one** dominant element.

## Solution Approach
We use two hash maps to track element frequencies before and after the split.
1. **Step 1:** Store the frequency of all elements in `secondMap`.
2. **Step 2:** Iterate through `nums`, updating `firstMap` and `secondMap` at each index.
3. **Step 3:** Check if both subarrays have the same dominant element.
4. **Step 4:** If a valid split is found, return the index; otherwise, return `-1`.

## Code Implementation (Java)
```java
import java.util.*;

class Solution {
    public int minimumIndex(List<Integer> nums) {
        Map<Integer, Integer> firstMap = new HashMap<>();
        Map<Integer, Integer> secondMap = new HashMap<>();
        int n = nums.size();

        // Add all elements of nums to secondMap
        for (int num : nums) {
            secondMap.put(num, secondMap.getOrDefault(num, 0) + 1);
        }

        for (int index = 0; index < n; index++) {
            // Create split at current index
            int num = nums.get(index);
            secondMap.put(num, secondMap.get(num) - 1);
            firstMap.put(num, firstMap.getOrDefault(num, 0) + 1);

            // Check if valid split
            if (
                firstMap.get(num) * 2 > index + 1 &&
                secondMap.get(num) * 2 > n - index - 1
            ) {
                return index;
            }
        }
        
        // No valid split exists
        return -1;
    }
}
```

## Complexity Analysis
- **Time Complexity:** `O(n)`, as we iterate through `nums` twice.
- **Space Complexity:** `O(n)`, due to the two hash maps used.

## Alternative Approaches
- A more optimized solution could involve reducing the use of extra space by tracking frequencies differently.

## Related Topics
- Hash Maps
- Prefix Sum
- Frequency Counting

    
