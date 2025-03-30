# Partition Labels - LeetCode 763

## Problem Statement
You are given a string `s`. We want to partition the string into as many parts as possible so that each letter appears in at most one part.

For example, the string `"ababcc"` can be partitioned into `["abab", "cc"]`, but partitions such as `["aba", "bcc"]` or `["ab", "ab", "cc"]` are invalid.

The partition should be done so that after concatenating all the parts in order, the resultant string should be `s`.

Return a list of integers representing the size of these parts.

### Example 1:
```plaintext
Input: s = "ababcbacadefegdehijhklij"
Output: [9,7,8]
Explanation:
The partition is "ababcbaca", "defegde", "hijhklij".
Each letter appears in at most one part.
```

### Example 2:
```plaintext
Input: s = "eccbbbbdec"
Output: [10]
```

### Constraints:
- `1 <= s.length <= 500`
- `s` consists of lowercase English letters.

---

## Solution Approach
The solution uses a greedy approach with the following steps:
1. **Track the last occurrence of each character** in the string.
2. **Iterate through the string** while keeping track of the farthest last occurrence within the current partition.
3. **Whenever the current index matches the farthest last occurrence**, finalize the partition and start a new one.

---

## Java Solution
```java
import java.util.*;

class Solution {
    public List<Integer> partitionLabels(String s) {
        // Stores the last index of each character in 's'
        int[] lastOccurrence = new int[26];
        for (int i = 0; i < s.length(); ++i) {
            lastOccurrence[s.charAt(i) - 'a'] = i;
        }

        int partitionEnd = 0, partitionStart = 0;
        List<Integer> partitionSizes = new ArrayList<>();
        for (int i = 0; i < s.length(); ++i) {
            partitionEnd = Math.max(partitionEnd, lastOccurrence[s.charAt(i) - 'a']);
            // End of the current partition
            if (i == partitionEnd) {
                partitionSizes.add(i - partitionStart + 1);
                partitionStart = i + 1;
            }
        }
        return partitionSizes;
    }
}
```

---

## Complexity Analysis
- **Time Complexity**: `O(N)`, where `N` is the length of the string. We iterate over `s` twice, once to store last occurrences and once to create partitions.
- **Space Complexity**: `O(1)`, since we use a fixed array of size `26`.

---

## How to Run
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/partition-labels.git
   ```
2. Navigate to the project folder:
   ```bash
   cd partition-labels
   ```
3. Compile and run the Java file:
   ```bash
   javac Solution.java && java Solution
   ```

---

## Contributions
Feel free to fork this repository and submit pull requests for improvements!

---
