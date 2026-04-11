# 🪢 Connect Ropes (Minimum Cost)

## 📌 Problem
- Given rope lengths,  
- connect all ropes into one rope with **minimum total cost**.

- 👉 Cost of joining two ropes = **sum of their lengths**

---

## 🧠 Key Idea (Greedy + Min Heap)

- 👉 Always connect **two smallest ropes first**  
- 👉 Why? → minimizes future cost  

---

## 🛠️ Approach

### 🔹 Step 1: Insert all ropes into Min Heap

- PriorityQueue (default = min heap)

---

### 🔹 Step 2: Repeat until one rope left
- take two smallest
- sum = a + b
- add cost
- push sum back
---

## 💻  Code

```java
import java.util.PriorityQueue;

public class Solution {

    public static long connectRopes(int[] arr) {

        PriorityQueue<Integer> pq = new PriorityQueue<>();

        // Insert all ropes
        for (int num : arr) {
            pq.add(num);
        }

        long cost = 0;

        // Connect ropes
        while (pq.size() > 1) {
            int a = pq.poll();
            int b = pq.poll();

            int sum = a + b;
            cost += sum;

            pq.add(sum);
        }

        return cost;
    }
}
```
----
### ⏱️ Time Complexity
- O(N log N)
- Insert → N log N
- Each merge → log N
### 📦 Space Complexity
- O(N)
- Heap stores elements
