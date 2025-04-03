# 🚀 Maximum Value of an Ordered Triplet II (LeetCode 2874)

## Problem Statement  
You are given a **0-indexed** integer array `nums`.  

Return the **maximum value** over all triplets of indices `(i, j, k)` such that `i < j < k`. If all such triplets have a **negative value**, return `0`.  

The value of a triplet of indices `(i, j, k)` is calculated as:  
\[
(nums[i] - nums[j]) * nums[k]
\]

### Example 1  
**Input:**  
```plaintext
nums = [12,6,1,2,7]
```
**Output:**  
```plaintext
77
```
**Explanation:**  
The value of the triplet `(0, 2, 4)` is:  
\[
(12 - 1) * 7 = 77
\]
It can be shown that this is the maximum possible value.

---

### Example 2  
**Input:**  
```plaintext
nums = [1,10,3,4,19]
```
**Output:**  
```plaintext
133
```
**Explanation:**  
The value of the triplet `(1, 2, 4)` is:  
\[
(10 - 3) * 19 = 133
\]
No other triplet gives a higher value.

---

### Example 3  
**Input:**  
```plaintext
nums = [1,2,3]
```
**Output:**  
```plaintext
0
```
**Explanation:**  
The only valid triplet `(0, 1, 2)` has a negative value:  
\[
(1 - 2) * 3 = -3
\]
So, the result is `0`.

---

## 💡 Approach  
1. **Precompute left max and right max values**  
   - `leftMax[i]`: Maximum value from the left up to index `i`.
   - `rightMax[i]`: Maximum value from the right up to index `i`.

2. **Iterate through all possible middle elements (`j`)**  
   - Compute `(leftMax[j] - nums[j]) * rightMax[j]`.
   - Track the maximum result.

---

## 📝 Code Implementation (Java)
```java
public class Solution {
    public long maximumTripletValue(int[] nums) {
        int n = nums.length;
        int[] leftMax = new int[n];
        int[] rightMax = new int[n];
        
        for (int i = 1; i < n; i++) {
            leftMax[i] = Math.max(leftMax[i - 1], nums[i - 1]);
            rightMax[n - 1 - i] = Math.max(rightMax[n - i], nums[n - i]);
        }
        
        long res = 0;
        for (int j = 1; j < n - 1; j++) {
            res = Math.max(res, (long) (leftMax[j] - nums[j]) * rightMax[j]);
        }
        return res;
    }
}
```

---

## 🔥 Complexity Analysis  
- **Time Complexity:** `O(n)`, as we traverse the array **three times**.  
- **Space Complexity:** `O(n)`, for storing `leftMax` and `rightMax`.  

---

## 📌 Usage  
1. Clone the repository or copy the code.  
2. Run the Java file in any Java environment.  
3. Input an array of integers and get the **maximum ordered triplet value**.  

---

## 📜 License  
This project is licensed under the **MIT License**.  

---

## 🚀 Contributing  
Feel free to contribute by improving the algorithm or optimizing the space complexity!  

---

🔗 **Happy Coding! 🚀**
