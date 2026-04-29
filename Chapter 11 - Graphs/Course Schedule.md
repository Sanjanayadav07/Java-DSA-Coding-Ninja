# Course Schedule / Can Finish Tasks

## 📌 Problem
Given prerequisite relations between tasks/courses,
determine whether all tasks can be completed.

---

## 🧠 Approach
- Model courses as Directed Graph
- Use DFS + Recursion Stack
- If cycle exists → impossible to finish all tasks

---
## Code 
```
import java.util.*;
import java.io.*;

public class Solution {

    public static String canFinish(ArrayList<ArrayList<Integer>> arr, int n, int m) {

        // Step 1: Create adjacency list
        List<List<Integer>> graph = new ArrayList<>();

        for (int i = 0; i < n; i++) {
            graph.add(new ArrayList<>());
        }

        // Step 2: Add directed edges
        for (int i = 0; i < m; i++) {

            int u = arr.get(i).get(0) - 1; // convert to 0-based indexing
            int v = arr.get(i).get(1) - 1;

            graph.get(u).add(v);
        }

        boolean[] visited = new boolean[n];
        boolean[] inRecStack = new boolean[n];

        // Step 3: DFS for every component
        for (int i = 0; i < n; i++) {

            if (!visited[i]) {

                if (dfs(graph, i, visited, inRecStack)) {
                    return "No"; // cycle exists
                }
            }
        }

        return "Yes"; // no cycle
    }

    // DFS Cycle Detection
    private static boolean dfs(List<List<Integer>> graph, int node,
                               boolean[] visited,
                               boolean[] inRecStack) {

        visited[node] = true;
        inRecStack[node] = true;

        for (int neighbor : graph.get(node)) {

            // Visit unvisited node
            if (!visited[neighbor]) {

                if (dfs(graph, neighbor, visited, inRecStack)) {
                    return true;
                }
            }

            // Back edge found
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
