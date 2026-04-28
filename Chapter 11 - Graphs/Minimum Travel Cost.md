# Minimum Spanning Tree (Kruskal’s Algorithm)

## 📌 Problem
Find a Minimum Spanning Tree (MST) of a weighted undirected graph.

---

## 🧠 Approach
- Sort all edges by weight
- Use Disjoint Set (Union-Find)
- Pick smallest edge that does NOT form a cycle

---

## Code
```
import java.util.*;

public class Solution {

    // Edge class
    static class Edge {
        int u, v, w;

        Edge(int u, int v, int w) {
            this.u = u;
            this.v = v;
            this.w = w;
        }
    }

    // Find with Path Compression
    public static int findParent(int[] parent, int v) {
        if (parent[v] != v) {
            parent[v] = findParent(parent, parent[v]);
        }
        return parent[v];
    }

    // Union by Rank
    public static void union(int[] parent, int[] rank, int x, int y) {
        if (rank[x] > rank[y]) {
            parent[y] = x;
        } else if (rank[x] < rank[y]) {
            parent[x] = y;
        } else {
            parent[y] = x;
            rank[x]++;
        }
    }

    public static int[][] findMST(int[][] edges, int n, int m) {

        // Step 1: Store edges
        List<Edge> list = new ArrayList<>();
        for (int i = 0; i < m; i++) {
            list.add(new Edge(edges[i][0], edges[i][1], edges[i][2]));
        }

        // Step 2: Sort edges by weight
        Collections.sort(list, (a, b) -> a.w - b.w);

        // Step 3: Initialize DSU
        int[] parent = new int[n + 1];
        int[] rank = new int[n + 1];

        for (int i = 0; i <= n; i++) {
            parent[i] = i;
            rank[i] = 0;
        }

        List<int[]> result = new ArrayList<>();

        // Step 4: Process edges
        for (Edge edge : list) {

            int x = findParent(parent, edge.u);
            int y = findParent(parent, edge.v);

            // If no cycle → include edge
            if (x != y) {
                result.add(new int[]{edge.u, edge.v, edge.w});
                union(parent, rank, x, y);
            }
        }

        // Step 5: Convert to array
        int[][] mst = new int[result.size()][3];
        for (int i = 0; i < result.size(); i++) {
            mst[i] = result.get(i);
        }

        return mst;
    }
}
```
---


## ⚡ Complexity
- Time: O(E log E)
- Space: O(V)
