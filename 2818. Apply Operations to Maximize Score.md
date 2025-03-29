# Maximum Score by Applying Operations

## Problem Statement
You are given an array `nums` of `n` positive integers and an integer `k`.

Initially, you start with a score of `1`. You have to maximize your score by applying the following operation at most `k` times:

- Choose any non-empty subarray `nums[l, ..., r]` that you haven't chosen previously.
- Choose an element `x` from `nums[l, ..., r]` with the highest prime score. If multiple such elements exist, choose the one with the smallest index.
- Multiply your score by `x`.

The prime score of an integer `x` is equal to the number of distinct prime factors of `x`.

Return the **maximum possible score** after applying at most `k` operations.

### Constraints:
- `1 <= nums.length == n <= 10^5`
- `1 <= nums[i] <= 10^5`
- `1 <= k <= min(n * (n + 1) / 2, 10^9)`

## Solution Approach
This solution follows an optimized approach using **prime factorization**, **monotonic stacks**, **priority queues**, and **modular exponentiation**.

### Steps:
1. **Compute Prime Scores**: For each number in `nums`, count its distinct prime factors.
2. **Find Next and Previous Dominant Elements**: Using a monotonic stack, determine the closest indices where the prime score is higher.
3. **Compute Subarray Contribution**: Determine how many subarrays each number is dominant in.
4. **Process in Descending Order**: Use a priority queue to pick elements in decreasing order of value and apply operations efficiently.
5. **Use Modular Exponentiation**: Since the result can be large, compute the score using fast exponentiation modulo `10^9 + 7`.

## Code Implementation
```java
class Solution {
    final int MOD = 1000000007;

    public int maximumScore(List<Integer> nums, int k) {
        int n = nums.size();
        List<Integer> primeScores = new ArrayList<>(Collections.nCopies(n, 0));

        // Calculate prime scores
        for (int index = 0; index < n; index++) {
            int num = nums.get(index);
            for (int factor = 2; factor <= Math.sqrt(num); factor++) {
                if (num % factor == 0) {
                    primeScores.set(index, primeScores.get(index) + 1);
                    while (num % factor == 0) num /= factor;
                }
            }
            if (num >= 2) primeScores.set(index, primeScores.get(index) + 1);
        }

        // Compute next and previous dominant indices
        int[] nextDominant = new int[n];
        int[] prevDominant = new int[n];
        Arrays.fill(nextDominant, n);
        Arrays.fill(prevDominant, -1);
        Stack<Integer> stack = new Stack<>();

        for (int index = 0; index < n; index++) {
            while (!stack.isEmpty() && primeScores.get(stack.peek()) < primeScores.get(index)) {
                nextDominant[stack.pop()] = index;
            }
            if (!stack.isEmpty()) prevDominant[index] = stack.peek();
            stack.push(index);
        }

        // Compute number of subarrays where each element is dominant
        long[] numOfSubarrays = new long[n];
        for (int index = 0; index < n; index++) {
            numOfSubarrays[index] = ((long) nextDominant[index] - index) * (index - prevDominant[index]);
        }

        // Process elements in descending order of value
        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> b[0] == a[0] ? Integer.compare(a[1], b[1]) : Integer.compare(b[0], a[0]));
        for (int index = 0; index < n; index++) {
            pq.offer(new int[]{nums.get(index), index});
        }

        long score = 1;
        while (k > 0) {
            int[] top = pq.poll();
            int num = top[0], index = top[1];
            long operations = Math.min((long) k, numOfSubarrays[index]);
            score = (score * power(num, operations)) % MOD;
            k -= operations;
        }
        return (int) score;
    }

    // Fast modular exponentiation
    private long power(long base, long exponent) {
        long res = 1;
        while (exponent > 0) {
            if (exponent % 2 == 1) res = (res * base) % MOD;
            base = (base * base) % MOD;
            exponent /= 2;
        }
        return res;
    }
}
```

## Complexity Analysis
- **Computing Prime Scores**: `O(n * sqrt(m))` where `m` is the maximum value in `nums`.
- **Finding Dominant Elements**: `O(n)` using monotonic stacks.
- **Processing via Priority Queue**: `O(n log n)`.
- **Binary Exponentiation**: `O(log k)` per multiplication.

Overall, the approach runs efficiently in **O(n log n + n sqrt(m))**.

## Example Walkthrough
### Example 1
**Input:**
```plaintext
nums = [8,3,9,3,8], k = 2
```
**Output:**
```plaintext
81
```
**Explanation:**
1. Choose `nums[2] = 9`, score = `1 * 9 = 9`.
2. Choose `nums[2]` again, score = `9 * 9 = 81`.

### Example 2
**Input:**
```plaintext
nums = [19,12,14,6,10,18], k = 3
```
**Output:**
```plaintext
4788
```
**Explanation:**
1. Choose `nums[0] = 19`, score = `1 * 19 = 19`.
2. Choose `nums[5] = 18`, score = `19 * 18 = 342`.
3. Choose `nums[2] = 14`, score = `342 * 14 = 4788`.

## Conclusion
This solution leverages prime factorization, monotonic stacks, priority queues, and modular exponentiation to efficiently maximize the score. 🚀

