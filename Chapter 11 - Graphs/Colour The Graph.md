# 🎨 Bipartite Graph Check (BFS)

## 📌 Problem
Check whether a given graph is **Bipartite** or not.

---

## 🧠 Key Idea

👉 A graph is bipartite if:
- We can color all nodes using **2 colors**
- No two adjacent nodes have same color

---

## ⚡ Concept

Use:
- 🔵 Color 1
- 🔴 Color 0

If any edge connects same color nodes → ❌ Not Bipartite

---

## 🛠️ Approach (BFS)

- Step 1: Start BFS from unvisited node  
- Step 2: Assign color 1  
- Step 3: Assign opposite color to neighbors  
- Step 4: Check conflicts  

---

## 💻 Code

```java
import java.io.*;
import java.util.*;

public class Solution {

    // BFS check for bipartite
    public static boolean bfs(ArrayList<ArrayList<Integer>> adj, int[] colour, int start) {

        Queue<Integer> q = new LinkedList<>();

        colour[start] = 1; // first color
        q.add(start);

        while (!q.isEmpty()) {

            int node = q.poll();

            for (int child : adj.get(node)) {

                // not visited
                if (colour[child] == -1) {
                    colour[child] = 1 - colour[node]; // alternate color
                    q.add(child);
                }

                // conflict found
                else if (colour[child] == colour[node]) {
                    return false;
                }
            }
        }

        return true;
    }

    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        String[] ve = br.readLine().split(" ");
        int vertices = Integer.parseInt(ve[0]);
        int edges = Integer.parseInt(ve[1]);

        ArrayList<ArrayList<Integer>> adj = new ArrayList<>();

        for (int i = 0; i <= vertices; i++) {
            adj.add(new ArrayList<>());
        }

        for (int i = 0; i < edges; i++) {
            String[] uv = br.readLine().split(" ");
            int u = Integer.parseInt(uv[0]);
            int v = Integer.parseInt(uv[1]);

            adj.get(u).add(v);
            adj.get(v).add(u);
        }

        int[] colour = new int[vertices + 1];
        Arrays.fill(colour, -1);

        boolean isBipartite = true;

        for (int i = 1; i <= vertices; i++) {
            if (colour[i] == -1) {
                if (!bfs(adj, colour, i)) {
                    isBipartite = false;
                    break;
                }
            }
        }

        System.out.println(isBipartite ? "YES" : "NO");
    }
}
```
---
### ⏱️ Time Complexity
- O(V + E)
- Each node visited once
- Each edge processed once
### 📦 Space Complexity
- O(V)
- Color array + queue
