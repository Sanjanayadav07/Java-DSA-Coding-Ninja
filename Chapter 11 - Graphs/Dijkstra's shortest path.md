# 🚀 Dijkstra Algorithm (Shortest Path)

## 📌 Problem
Given a weighted graph,  
find **shortest distance from source to all vertices**.

---

## 🧠 Key Idea

👉 Use **Greedy + Min Heap (PriorityQueue)**  
👉 Always pick node with **smallest distance**

---

## 🛠️ Approach

### 🔹 Step 1: Build Graph

- Adjacency List → (node, weight)


---

### 🔹 Step 2: Initialize


- dist[source] = 0
- others = ∞


---

### 🔹 Step 3: Use Min Heap


- Store → {distance, node}


---

### 🔹 Step 4: Relaxation


- if (d + weight < dist[adjNode])
- update distance


---

## 💻 Code

```java
import java.util.*;

public class Solution {
	
	public static ArrayList<Integer> dijkstra(ArrayList<ArrayList<Integer>> vec, int vertices, int edges, int source){
		
		ArrayList<ArrayList<int[]>> adj = new ArrayList<>();
		
		for(int i = 0; i < vertices; i++){
			adj.add(new ArrayList<>());
		}
		
		for(ArrayList<Integer> edge : vec){
			int u = edge.get(0);
			int v = edge.get(1);
			int w = edge.get(2);
			
			adj.get(u).add(new int[]{v, w});
			adj.get(v).add(new int[]{u, w});
		}
		
		int[] dist = new int[vertices];
		Arrays.fill(dist, Integer.MAX_VALUE);
		
		PriorityQueue<int[]> pq = new PriorityQueue<>((a,b) -> a[0] - b[0]);
		
		dist[source] = 0;
		pq.offer(new int[]{0, source});
		
		while(!pq.isEmpty()){
			
			int[] current = pq.poll();
			int d = current[0];
			int node = current[1];

			// Optimization (skip outdated entries)
			if(d > dist[node]) continue;
			
			for(int[] neighbor : adj.get(node)){
				
				int adjNode = neighbor[0];
				int weight = neighbor[1];
				
				if(d + weight < dist[adjNode]){
					dist[adjNode] = d + weight;
					pq.offer(new int[]{dist[adjNode], adjNode});
				}
			}
		}
		
		ArrayList<Integer> result = new ArrayList<>();
		for(int i = 0; i < vertices; i++){
			result.add(dist[i]);
		}
		
		return result;
	}
}
```
---
### ⏱️ Time Complexity
- O((V + E) log V)
- Each edge processed
- Heap operations → log V
###📦 Space Complexity
- O(V + E)
- Graph + distance array
