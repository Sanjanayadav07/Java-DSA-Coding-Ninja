
## Problem Statement

- Given a directed graph with V vertices and E edges, and a starting node S, find the total number of nodes reachable from S (including itself).
- Return the result modulo 10^9 +7.
---
## Approach
- Represent the graph using an adjacency list.
- Use DFS (Depth First Search) to traverse the graph.
- Use a DP array (memoization) to store already computed results.
- For each node:
   - Count itself as 1
   - Add results of all its children

---
## Formula:

- dp[node] = 1 + sum of dp[child]

---
## Code (Java)
```
import java.util.*;

public class Solution {
    static final int MOD = 1_000_000_007;

    public static int solve(List<List<Integer>> adj, int[] dp, int node) {
        if (dp[node] != -1) {
            return dp[node];
        }

        int ans = 1;

        for (int child : adj.get(node)) {
            ans = (ans + solve(adj, dp, child)) % MOD;
        }

        dp[node] = ans;
        return ans;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int V = sc.nextInt();
        int E = sc.nextInt();
        int S = sc.nextInt();

        List<List<Integer>> adj = new ArrayList<>();
        for (int i = 0; i <= V; i++) {
            adj.add(new ArrayList<>());
        }

        for (int i = 0; i < E; i++) {
            int u = sc.nextInt();
            int v = sc.nextInt();
            adj.get(u).add(v);
        }

        int[] dp = new int[V + 1];
        Arrays.fill(dp, -1);

        int result = solve(adj, dp, S);
        System.out.println(result);

        sc.close();
    }
}
```
---
### Time Complexity
- O(V + E)
### Space Complexity
- O(V + E)
