# 🔗 Strongly Connected Components (Kosaraju’s Algorithm)

## 📌 Problem
Find all **Strongly Connected Components (SCCs)** in a directed graph.

👉 SCC = group of nodes where  
every node is reachable from every other node

---

## 🧠 Key Idea

👉 Use **2 DFS + Stack + Reverse Graph**

---

## ⚡ Steps (Kosaraju Algorithm)

### 🔹 Step 1: DFS + Stack (Finish Time Order)

👉 Push node into stack **after visiting all neighbors**


dfsFill → stack me order store hota hai


---

### 🔹 Step 2: Reverse Graph

👉 All edges reverse kar do


u → v becomes v → u


---

### 🔹 Step 3: DFS on Reversed Graph

👉 Stack se node pop karo  
👉 DFS chalao → ek SCC mil jayega  

---

## 💻 Code

```java
import java.util.*;

public class Solution {

    private static void dfsFill(int u, List<List<Integer>> adj, boolean[] visited, Stack<Integer> st) {
        visited[u] = true;

        for (int v : adj.get(u)) {
            if (!visited[v]) {
                dfsFill(v, adj, visited, st);
            }
        }

        st.push(u);
    }

    private static void dfsTraverse(int u, List<List<Integer>> revAdj, boolean[] visited, List<Integer> component) {
        visited[u] = true;
        component.add(u);

        for (int v : revAdj.get(u)) {
            if (!visited[v]) {
                dfsTraverse(v, revAdj, visited, component);
            }
        }
    }

    public static List<List<Integer>> stronglyConnectedComponents(int n, int[][] edges) {

        List<List<Integer>> adj = new ArrayList<>();
        for (int i = 0; i < n; i++) adj.add(new ArrayList<>());

        for (int[] edge : edges) {
            adj.get(edge[0]).add(edge[1]);
        }

        boolean[] visited = new boolean[n];
        Stack<Integer> st = new Stack<>();

        for (int i = 0; i < n; i++) {
            if (!visited[i]) {
                dfsFill(i, adj, visited, st);
            }
        }

        // Reverse graph
        List<List<Integer>> revAdj = new ArrayList<>();
        for (int i = 0; i < n; i++) revAdj.add(new ArrayList<>());

        for (int u = 0; u < n; u++) {
            for (int v : adj.get(u)) {
                revAdj.get(v).add(u);
            }
        }

        Arrays.fill(visited, false);
        List<List<Integer>> result = new ArrayList<>();

        while (!st.isEmpty()) {
            int node = st.pop();

            if (!visited[node]) {
                List<Integer> component = new ArrayList<>();
                dfsTraverse(node, revAdj, visited, component);
                result.add(component);
            }
        }

        return result;
    }
}
```
---
### ⏱️ Time Complexity
- O(V + E)
- 2 DFS traversals
- Graph reverse
### 📦 Space Complexity
- O(V + E)
- Graph + stack + visited
