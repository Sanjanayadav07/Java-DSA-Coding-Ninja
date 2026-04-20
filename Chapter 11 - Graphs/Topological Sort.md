# 📊 Topological Sort (DFS + Stack)

## 📌 Problem
Given a **Directed Acyclic Graph (DAG)**,  
find a linear ordering such that:

👉 For every edge `u → v`,  
`u` comes **before** `v`

---

## 🧠 Key Idea

👉 Use **DFS + Stack**

✔ Visit all nodes  
✔ Push node **after visiting its neighbors**  
✔ Reverse order → Topological Sort  

---

## 🛠️ Approach

### 🔹 Step 1: Build Graph

- Adjacency List (Directed)
---

### 🔹 Step 2: DFS Traversal

👉 For each unvisited node:
- Visit all neighbors first  
- Then push node into stack  
---

### 🔹 Step 3: Get Answer
- Pop from stack → Topological order
---

## 💻 Code

```java
import java.util.*;

public class Solution 
{
    static void dfs(ArrayList<ArrayList<Integer>> adj, int u, boolean[] visited, Stack<Integer> st)
    {
        visited[u] = true;

        for(int v : adj.get(u))
        {
            if(!visited[v])
            {
                dfs(adj, v, visited, st);
            }
        }

        // push after visiting neighbors
        st.push(u);
    }

    public static ArrayList<Integer> topologicalSort(ArrayList<ArrayList<Integer>> edges, int v, int e) 
    {
        ArrayList<ArrayList<Integer>> adj = new ArrayList<>();

        for(int i = 0; i < v; i++)
        {
            adj.add(new ArrayList<>());
        }

        for(ArrayList<Integer> edge : edges)
        {
            int u = edge.get(0);
            int w = edge.get(1);
            adj.get(u).add(w);
        }

        boolean[] visited = new boolean[v];
        Stack<Integer> st = new Stack<>();

        for(int i = 0; i < v; i++)
        {
            if(!visited[i])
            {
                dfs(adj, i, visited, st);
            }
        }

        ArrayList<Integer> result = new ArrayList<>();

        while(!st.isEmpty())
        {
            result.add(st.pop());
        }

        return result;
    }
}
```
---

### ⏱️ Time Complexity
- O(V + E)
- Each node + edge visited once
### 📦 Space Complexity
- O(V)
- Visited + Stack
