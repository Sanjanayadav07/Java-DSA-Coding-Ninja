# 🌳 Check if Graph is a Tree

## 📌 Problem
Given an undirected graph, check whether it is a **Tree** or not.

---

## 🧠 Key Idea

A graph is a **Tree** if:

- ✔ It has **no cycles**  
- ✔ It is **connected**  
- ✔ It has exactly:


E = V - 1


Where:
- `V` = number of vertices  
- `E` = number of edges  

---

## ⚡ Your Approach (Edge Counting Trick)

- 👉 Count total edges from adjacency list  
- 👉 Since graph is undirected → each edge is counted twice  

- So:
- E = total_count / 2
- Then check:
- E == V - 1
---

## 💻  Code

```java
import java.util.ArrayList;
import java.util.Scanner;

public class Solution {

    public static boolean isTree(ArrayList<ArrayList<Integer>> adj, int V) {

        int E = 0;

        // Count edges (twice in undirected graph)
        for (int i = 0; i < adj.size(); i++) {
            for (int j = 0; j < adj.get(i).size(); j++) {
                E++;
            }
        }

        E = E / 2; // because undirected graph

        return (E == V - 1);
    }

    public static void main(String[] args) {

        Scanner s = new Scanner(System.in);
        int V = s.nextInt();
        int E = s.nextInt();

        ArrayList<ArrayList<Integer>> adj = new ArrayList<>();

        for (int i = 0; i < V; i++) {
            adj.add(new ArrayList<>());
        }

        for (int i = 0; i < E; i++) {
            int x = s.nextInt();
            int y = s.nextInt();

            adj.get(x).add(y);
            adj.get(y).add(x);
        }

        if (isTree(adj, V))
            System.out.println("True");
        else
            System.out.println("False");
    }
}
```
---
### ⏱️ Time Complexity
- O(V + E)
- Traversing adjacency list once
### 📦 Space Complexity
- O(1)
- No extra data structures used
