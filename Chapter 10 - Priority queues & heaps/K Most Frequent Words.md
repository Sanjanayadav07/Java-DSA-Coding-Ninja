# 🔥 K Most Frequent Words

## 📌 Problem
Given an array of words, return the **K most frequent words**.

👉 If frequencies are same → return **lexicographically smaller word first**

---

## 🧠 Key Idea

1. Count frequency using **HashMap**
2. Use **Max Heap (Priority Queue)**:
   - Higher frequency → higher priority  
   - Same frequency → lexicographically smaller first  

---

## 🛠️ Approach

### Step 1: Count frequencies

- count.put(word, count.getOrDefault(word, 0) + 1)


---

### Step 2: Build Max Heap with custom comparator


- (a, b) -> {
- if(freq same) → lexicographically smaller first
- else → higher frequency first
 }


---

### Step 3: Extract top K words
- while(k-- > 0):
- remove from heap
---

## 💻  Code

```java
import java.util.*;

public class Solution {
	
	public static List<String> kMostFreqWords(String[] words, int k) {
		
		Map<String, Integer> count = new HashMap<>();

		// Max Heap
		PriorityQueue<Map.Entry<String, Integer>> queue =
			new PriorityQueue<>((a, b) -> {
				if (a.getValue().equals(b.getValue()))
					return a.getKey().compareTo(b.getKey()); // lexicographically smaller
				return b.getValue() - a.getValue(); // higher frequency first
			});

		List<String> ans = new ArrayList<>();

		// Step 1: Count frequency
		for (String w : words) {
			count.put(w, count.getOrDefault(w, 0) + 1);
		}

		// Step 2: Add to heap
		for (Map.Entry<String, Integer> e : count.entrySet()) {
			queue.add(e);
		}

		// Step 3: Get top k
		while (k-- > 0) {
			ans.add(queue.poll().getKey());
		}

		return ans;
	}
}

```
---
### ⏱️ Time Complexity
- O(N log N)
- Counting → O(N)
- Heap insert → O(N log N)
- Extract K → O(K log N)
### 📦 Space Complexity
- O(N)

⏱️ Optimized Complexity
Time: O(N log K)
Space: O(N)
