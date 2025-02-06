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
            
