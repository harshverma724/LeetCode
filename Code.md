# Most Profitable Path in a Tree

## Problem Statement
There is an undirected tree with `n` nodes labeled from `0` to `n - 1`, rooted at node `0`. Each node has a gate that requires either a price to open (if negative) or gives a reward (if positive). The game involves two players:

- **Alice** starts at node `0` and moves towards some leaf node.
- **Bob** starts at `bob` and moves towards node `0`.
- Both move simultaneously and can share the cost/reward of a gate if they reach a node at the same time.

The goal is to maximize Alice's net income as she travels towards an optimal leaf node.

## Example

### Input:
```plaintext
edges = [[0,1],[1,2],[1,3],[3,4]]
bob = 3
amount = [-2,4,2,-4,6]
```

### Output:
```plaintext
6
```

### Explanation:
Alice follows the best path and collects a net income of `6`.

## Constraints
- `2 <= n <= 10^5`
- `edges.length == n - 1`
- `0 <= ai, bi < n`
- `ai != bi`
- `1 <= bob < n`
- `amount[i]` is an even integer in `[-10^4, 10^4]`

## Solution Approach
The solution involves:
1. **Building the Tree**: Constructing an adjacency list representation of the tree.
2. **Finding Bob's Path**: Using DFS to determine the path Bob takes to reach node `0`.
3. **BFS for Alice**: Using BFS to simulate Alice's journey while maximizing her net income.

## Code Implementation
```java
class Solution {
    public int mostProfitablePath(int[][] edges, int bob, int[] amount) {
        int n = amount.length, maxIncome = Integer.MIN_VALUE;
        tree = new ArrayList<>();
        bobPath = new HashMap<>();
        visited = new boolean[n];
        Queue<int[]> nodeQueue = new LinkedList<>();
        nodeQueue.add(new int[] { 0, 0, 0 });
        for (int i = 0; i < n; i++) {
            tree.add(new ArrayList<>());
        }

        for (int[] edge : edges) {
            tree.get(edge[0]).add(edge[1]);
            tree.get(edge[1]).add(edge[0]);
        }

        findBobPath(bob, 0);

        Arrays.fill(visited, false);
        while (!nodeQueue.isEmpty()) {
            int[] node = nodeQueue.poll();
            int sourceNode = node[0], time = node[1], income = node[2];

            if (!bobPath.containsKey(sourceNode) || time < bobPath.get(sourceNode)) {
                income += amount[sourceNode];
            } else if (time == bobPath.get(sourceNode)) {
                income += amount[sourceNode] / 2;
            }

            if (tree.get(sourceNode).size() == 1 && sourceNode != 0) {
                maxIncome = Math.max(maxIncome, income);
            }
            for (int adjacentNode : tree.get(sourceNode)) {
                if (!visited[adjacentNode]) {
                    nodeQueue.add(new int[] { adjacentNode, time + 1, income });
                }
            }
            visited[sourceNode] = true;
        }
        return maxIncome;
    }

    private Map<Integer, Integer> bobPath;
    private boolean[] visited;
    private List<List<Integer>> tree;

    private boolean findBobPath(int sourceNode, int time) {
        bobPath.put(sourceNode, time);
        visited[sourceNode] = true;

        if (sourceNode == 0) {
            return true;
        }

        for (int adjacentNode : tree.get(sourceNode)) {
            if (!visited[adjacentNode]) {
                if (findBobPath(adjacentNode, time + 1)) {
                    return true;
                }
            }
        }
        bobPath.remove(sourceNode);
        return false;
    }
}
```

## How to Run
1. Clone the repository:
   ```sh
   git clone https://github.com/your-username/most-profitable-path.git
   cd most-profitable-path
   ```
2. Compile and run the Java program:
   ```sh
   javac Solution.java
   java Solution
   ```

## Complexity Analysis
- **Building the Tree**: `O(n)`
- **DFS for Bob’s Path**: `O(n)`
- **BFS for Alice’s Path**: `O(n)`
- **Overall Complexity**: `O(n)`

## Contributions
Feel free to submit pull requests to improve efficiency or add new features!

## License
This project is licensed under the MIT License.

