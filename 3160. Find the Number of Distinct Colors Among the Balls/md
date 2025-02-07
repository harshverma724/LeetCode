            import java.util.*;
            
            public class Solution {
                public int[] queryResults(int limit, int[][] queries) {
                    // This method was previously called distinctColors, but now it's queryResults.
                    Map<Integer, Integer> ballColors = new HashMap<>();
                    Set<Integer> distinctColors = new HashSet<>();
                    int n = queries.length;
                    int[] result = new int[n];
                
                    for (int i = 0; i < n; i++) {
                        int ball = queries[i][0];
                        int color = queries[i][1];
                    
                        // If ball was already colored with a different color, remove old color
                        if (ballColors.containsKey(ball)) {
                            int oldColor = ballColors.get(ball);
                            if (oldColor != color) {
                                distinctColors.remove(oldColor);
                            }
                        }
                    
                        // Assign the new color to the ball
                        ballColors.put(ball, color);
                    
                        // Add the new color to the set of distinct colors
                        distinctColors.add(color);
                    
                        // Store the result: number of distinct colors so far
                        result[i] = distinctColors.size();
                    }
                
                    return result;
                }
            
                public static void main(String[] args) {
                    Solution solution = new Solution();
                    
                    int limit = 4;
                    int[][] queries1 = {{1, 4}, {2, 5}, {1, 3}, {3, 4}};
                    int[] result1 = solution.queryResults(limit, queries1);  // This should work now
                    System.out.println(Arrays.toString(result1));  // Output: [1, 2, 2, 3]
                
                    int[][] queries2 = {{0, 1}, {1, 2}, {2, 2}, {3, 4}, {4, 5}};
                    int[] result2 = solution.queryResults(limit, queries2);  // This should work now
                    System.out.println(Arrays.toString(result2));  // Output: [1, 2, 2, 3, 4]
                }
            }
            
            
