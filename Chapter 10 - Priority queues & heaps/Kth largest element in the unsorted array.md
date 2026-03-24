# 🔺 Kth Largest Element 

## 📌 Problem
Given an array, find the **Kth largest element**.

---

## 🧠 Key Idea

Use a **Min Heap of size K**:

- Keep only **K largest elements**
- Smallest among them (top of heap) = **Kth largest**

---

## 🛠️ Approach

### Step 1: Create Min Heap
- PriorityQueue<Integer> pq = new PriorityQueue<>();
- 👉 Default Java PQ = **Min Heap**

---

### Step 2: Process Each Element
- For every element:
- 1️⃣ Add to heap  
- 2️⃣ If size > K → remove smallest  
- pq.add(num);
- if(pq.size() > K) pq.poll();


---

### Step 3: Answer
- pq.peek()
- 👉 This gives **Kth largest element**

---

## 💻  Code

```java
import java.util.*;

public class Solution {

    static int kthLargest(ArrayList<Integer> arr, int size, int K) {

        PriorityQueue<Integer> pq = new PriorityQueue<>();

        for (int num : arr) {
            pq.add(num);

            if (pq.size() > K) {
                pq.poll();
            }
        }

        return pq.peek();
    }
}
```
---
### ⏱️ Time Complexity
- O(N log K)
- Each insertion → O(log K)
- Total elements → N
### 📦 Space Complexity
- O(K)
- Heap stores only K elements
