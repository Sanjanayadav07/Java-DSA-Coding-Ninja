# 🔽 Kth Smallest Element (Using Min Heap)

## 📌 Problem
Find the **Kth smallest element** in an array.

---

## 🧠 Key Idea

👉 Use **Min Heap (Priority Queue)**  
- Smallest element always at top  
- Remove (k-1) elements → next = Kth smallest  

---

## 🛠️ Approach
### Step 1: Add all elements to Min Heap
- pq.add(num)

---

### Step 2: Remove (k-1) smallest elements

- for i = 1 to k-1:
- pq.poll()
---

### Step 3: Return top element

- return pq.peek()
---

## 💻 Code

```java
import java.util.PriorityQueue;

public class Solution {
    public static int kthSmallest(int n, int k, int[] arr) {
        
        if (k > n || k <= 0) {
            return -1;
        }

        PriorityQueue<Integer> pq = new PriorityQueue<>();

        // Step 1: Insert all elements
        for (int num : arr) {
            pq.add(num);
        }

        // Step 2: Remove k-1 elements
        for (int i = 1; i < k; i++) {
            pq.poll();
        }

        // Step 3: kth smallest
        return pq.peek();
    }
}
```
---
### ⏱️ Time Complexity
- O(N log N)
- Insert N elements → N log N
- Remove K elements → K log N
### 📦 Space Complexity
- O(N)
- Heap stores all elements
