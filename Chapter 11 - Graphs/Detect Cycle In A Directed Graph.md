# Detect Cycle in Directed Graph

## 📌 Problem
Given a directed graph, check if it contains a cycle.

---

## 🧠 Approach
- Use DFS traversal
- Maintain:
  - visited[] → nodes visited
  - recursion stack → current DFS path
- If we revisit a node already in recursion stack → cycle exists

---
## Code
```
import java.util.*;

public class Solution {

    public static boolean detectCycleInDirectedGraph(int n, ArrayList<ArrayList<Integer>> edges) {

        // Step 1: Create adjacency list
        ArrayList<ArrayList<Integer>> adj = new ArrayList<>();
        for (int i = 0; i <= n; i++) {
            adj.add(new ArrayList<>());
        }

        // Step 2: Fill adjacency list
        for (ArrayList<Integer> edge : edges) {
            int u = edge.get(0);
            int v = edge.get(1);
            adj.get(u).add(v);
        }

        boolean[] visited = new boolean[n + 1];
        boolean[] inRecStack = new boolean[n + 1];

        // Step 3: DFS for each component
        for (int i = 1; i <= n; i++) {
            if (!visited[i]) {
                if (dfs(adj, i, visited, inRecStack)) {
                    return true;
                }
            }
        }

        return false;
    }

    private static boolean dfs(ArrayList<ArrayList<Integer>> adj, int node,
                               boolean[] visited, boolean[] inRecStack) {

        visited[node] = true;
        inRecStack[node] = true;

        for (int neighbor : adj.get(node)) {

            // If not visited → DFS
            if (!visited[neighbor]) {
                if (dfs(adj, neighbor, visited, inRecStack)) {
                    return true;
                }
            }
            // If already in recursion stack → cycle found
            else if (inRecStack[neighbor]) {
                return true;
            }
        }

        // Backtrack
        inRecStack[node] = false;
        return false;
    }
}
```
----

## ⚡ Complexity
- Time: O(V + E)
- Space: O(V)
