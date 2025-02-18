Explanation:
Initial Check: If the strings are already equal, we return true immediately (no swap needed).
Find Differences: We loop through both strings and record the indices where the characters differ.
Conditions for Swap:
If there are exactly two differences, we check if swapping the characters at these two indices will make the strings equal.
We compare s1[i] with s2[j] and s1[j] with s2[i] to see if a swap can make the strings equal.
Return the Result: If the above conditions hold, return true, otherwise false.

            public class Solution {
                public boolean areAlmostEqual(String s1, String s2) {
                    // If the strings are already equal, no swap is needed
                    if (s1.equals(s2)) {
                        return true;
                    }
            
                    // Find all the indices where s1 and s2 differ
                    List<Integer> diffIndices = new ArrayList<>();
                    for (int i = 0; i < s1.length(); i++) {
                        if (s1.charAt(i) != s2.charAt(i)) {
                            diffIndices.add(i);
                        }
                    }
            
                    // If there are not exactly two differences, return false
                    if (diffIndices.size() != 2) {
                        return false;
                    }
            
                    // Get the indices where the strings differ
                    int i = diffIndices.get(0);
                    int j = diffIndices.get(1);
            
                    // Check if swapping the characters at i and j in s2 makes s1 equal to s2
                    return s1.charAt(i) == s2.charAt(j) && s1.charAt(j) == s2.charAt(i);
                }
            }
            
