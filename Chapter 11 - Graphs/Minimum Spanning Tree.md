# 🌳 Minimum Spanning Tree (Prim’s Algorithm)

## 📌 Problem
Given a weighted undirected graph,  
find **Minimum Spanning Tree (MST)**

👉 MST = subset of edges:
- Connects all vertices  
- No cycles  
- Minimum total weight  

---

## 🧠 Key Idea

👉 Use **Greedy + Min Heap (PriorityQueue)**  

- ✔ Always pick **minimum weight edge**  
- ✔ Expand tree step by step  

---

## 🛠️ Approach (Prim’s Algorithm)

### 🔹 Step 1: Build Graph

- Adjacency List → (node, weight)
---

### 🔹 Step 2: Initialize

- Start from node 0
- Mark all nodes unvisited

---

### 🔹 Step 3: Min Heap

- Store → {weight, node}
---

### 🔹 Step 4: Process

- Pick smallest edge  
- If node not in MST:
  - Add weight to answer  
  - Mark visited  
  - Push neighbors  

---

## 💻 Code

```java
import java.util.*;

public class Solution {

	public static int minimumSpanningTree(ArrayList<ArrayList<Integer>> edges, int n) {
		
		ArrayList<ArrayList<int[]>> adj = new ArrayList<>();

		for(int i = 0; i < n; i++){
			adj.add(new ArrayList<>());
		}

		for(ArrayList<Integer> edge : edges){
			int u = edge.get(0);
			int v = edge.get(1);
			int w = edge.get(2);

			adj.get(u).add(new int[]{v, w});
			adj.get(v).add(new int[]{u, w});
		}

		boolean[] inMST = new boolean[n];

		PriorityQueue<int[]> pq = new PriorityQueue<>((a,b) -> a[0] - b[0]);

		int sum = 0;

		pq.offer(new int[]{0, 0});

		while(!pq.isEmpty()){

			int[] curr = pq.poll();
			int wt = curr[0];
			int node = curr[1];

			if(inMST[node]) continue;

			inMST[node] = true;
			sum += wt;

			for(int[] neighbour : adj.get(node)){
				int nextNode = neighbour[0];
				int edgeWeight = neighbour[1];

				if(!inMST[nextNode]){
					pq.offer(new int[]{edgeWeight, nextNode});
				}
			}
		}

		return sum;
	}
}
```
---
### ⏱️ Time Complexity
- O((V + E) log V)
- Heap operations → log V
- Each edge processed
### 📦 Space Complexity
- O(V + E)
- Graph + heap
