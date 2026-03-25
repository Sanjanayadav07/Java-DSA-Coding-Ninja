# 🔺 Kth Largest Element in Stream

## 📌 Problem
Design a class that:

- Initializes with an array  
- Continuously adds elements  
- Returns **Kth largest element after each insertion**

---

## 🧠 Key Idea

Use a **Min Heap of size K**:

- 👉 Heap always stores **K largest elements**  
- 👉 Smallest among them = **Kth largest**

---

## 🛠️ Approach

### 🔹 Initialization

- Add all elements into heap  
- Maintain size ≤ K  


- if size > K → remove smallest


---

### 🔹 Add Operation

- When new element comes:

  - 1️⃣ Add element
  - 2️⃣ If size > K → remove smallest
  - 3️⃣ Return top of heap  

---

## 💻 Code

```java
import java.util.PriorityQueue;

public class Solution {

    public static class Kthlargest {

        private PriorityQueue<Integer> pq;
        private int k;

        public Kthlargest(int k, int[] arr) {
            this.k = k;
            pq = new PriorityQueue<>();

            // Initialize heap
            for (int num : arr) {
                pq.add(num);
                if (pq.size() > k) {
                    pq.poll();
                }
            }
        }

        public int add(int num) {

            pq.add(num);

            if (pq.size() > k) {
                pq.poll();
            }

            return pq.peek();
        }
    }
}
```
---
### ⏱️ Time Complexity
- Constructor → O(N log K)
- add() → O(log K)
### 📦 Space Complexity
- O(K)
