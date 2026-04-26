# Transitive Closure of a Graph

## 📌 Problem
Find reachability between every pair of vertices in a graph.

If there is a path from i → j, mark it as 1 else 0.

---

## 🧠 Approach
- Convert graph into adjacency matrix
- Apply Floyd-Warshall algorithm
- Check if path exists through intermediate node k

---
## code 
```

import java.util.*;

public class Solution 
{
    public static ArrayList<ArrayList<Integer>> findClosure(ArrayList<ArrayList<Integer>> adj, int v, int e) 
    {
        // Step 1: Create reachability matrix
        int[][] reach = new int[v][v];

        // Step 2: Every node can reach itself
        for (int i = 0; i < v; i++) {
            reach[i][i] = 1;
        }

        // Step 3: Fill direct edges
        for (int i = 0; i < v; i++) {
            for (int node : adj.get(i)) {
                reach[i][node] = 1;
            }
        }

        // Step 4: Floyd-Warshall Algorithm
        for (int k = 0; k < v; k++) {
            for (int i = 0; i < v; i++) {
                for (int j = 0; j < v; j++) {

                    // If path exists through k
                    if (reach[i][k] == 1 && reach[k][j] == 1) {
                        reach[i][j] = 1;
                    }
                }
            }
        }

        // Step 5: Convert to ArrayList format
        ArrayList<ArrayList<Integer>> result = new ArrayList<>();

        for (int i = 0; i < v; i++) {
            ArrayList<Integer> row = new ArrayList<>();
            for (int j = 0; j < v; j++) {
                row.add(reach[i][j]);
            }
            result.add(row);
        }

        return result;
    }
}
```
----

## ⚡ Complexity
- Time: O(V^3)
- Space: O(V^2)
