# 🧮 Sorted Matrix (Using Min Heap)

## 📌 Problem
- Given an `N x N` matrix,  
- return all elements in **sorted order**.

---

## 🧠 Key Idea

- 👉 Use **Min Heap (PriorityQueue)**  
- 👉 Insert all elements → extract in sorted order  

---

## 🛠️ Approach

### 🔹 Step 1: Traverse matrix

- Add every element into min heap


---

### 🔹 Step 2: Extract elements

- Remove from heap → always gives smallest element

---

## 💻 Code

```java
import java.util.*;

public class Solution {
	
	public static List<Integer> sortedMatrix(int[][] mat, int n) {

		PriorityQueue<Integer> pq = new PriorityQueue<>();

		// Add all elements to heap
		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n; j++) {
				pq.add(mat[i][j]);
			}
		}

		List<Integer> list = new ArrayList<>();

		// Extract sorted elements
		while (!pq.isEmpty()) {
			list.add(pq.poll());
		}

		return list;
	}
}
```
---
### ⏱️ Time Complexity
- O(N^2 log N)
- Total elements = N^2
- Each insert/remove → log N^2 = log N
### 📦 Space Complexity
- O(N^2)
- Heap stores all elements
