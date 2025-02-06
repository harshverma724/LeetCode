# Solution Approach for "Tuple with Same Product"

## Problem Overview

The problem asks to find the number of distinct tuples `(a, b, c, d)` in a given array of distinct positive integers `nums`, where:

- `a * b = c * d`, and
- All values in the tuple are distinct (`a != b != c != d`).

## Approach

### 1. **Calculate All Pairwise Products**

The first step is to generate all possible pairs `(a, b)` from the array `nums`. For each pair, we calculate the product `a * b`. This gives us potential candidates for products that we will later compare with other pairs.

### 2. **Count Occurrences of Each Product**

We store the frequency of each product in a **HashMap**. The key of the HashMap is the product, and the value is the count of how many times that product has appeared so far. This allows us to efficiently track how many pairs result in the same product.

- **Why a HashMap?**
  The HashMap allows us to quickly look up the frequency of any product and helps us keep track of the pair count in constant time.

### 3. **Valid Tuple Calculation**

Once we have the frequency of each product, we need to calculate the number of valid tuples. For every product that appears `k` times, we can form `k * (k - 1) / 2` distinct valid pairs of pairs. This formula comes from combinatorics and counts how many ways we can select two distinct pairs from `k` pairs.

However, for each valid tuple, there are **4 permutations** (since the tuple `(a, b, c, d)` can be rearranged in 4 different ways: `(a, b, c, d)`, `(a, c, b, d)`, `(a, d, b, c)`, and `(b, c, a, d)`).

Therefore, the total number of valid tuples for each product with `k` occurrences is:


            
            import java.util.HashMap;
            import java.util.Map;
            
            public class Solution {
                public int tupleSameProduct(int[] nums) {
                    Map<Integer, Integer> productCount = new HashMap<>();
                    int result = 0;
            
                    // Count all possible products of pairs
                    for (int i = 0; i < nums.length; i++) {
                        for (int j = i + 1; j < nums.length; j++) {
                            int product = nums[i] * nums[j];
                            productCount.put(product, productCount.getOrDefault(product, 0) + 1);
                        }
                    }
            
                    // Calculate number of tuples based on product count
                    for (int count : productCount.values()) {
                        if (count > 1) {
                            result += count * (count - 1) * 4;
                        }
                    }
            
                    return result;
                }
            
                public static void main(String[] args) {
                    Solution solution = new Solution();
                    int[] nums1 = {2, 3, 4, 6};
                    System.out.println(solution.tupleSameProduct(nums1)); // Output: 8
            
                    int[] nums2 = {1, 2, 4, 5, 10};
                    System.out.println(solution.tupleSameProduct(nums2)); // Output: 16
                }
            }
            
