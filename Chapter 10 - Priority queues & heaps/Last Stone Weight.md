
# 🪨 Last Stone Weight (Heap)

## 📌 Problem
- You have stones with positive weights  
- **Smash** two heaviest stones `a` and `b`:
  - If `a == b` → both destroyed  
  - Else → remaining stone `a - b` goes back  
- Find **weight of last stone**

---

## 🧠 Approach (Max Heap)
1. Push all stones into **Max-Heap**  
2. While heap size > 1:
   - Pop **two largest** `a` and `b`  
   - If `a != b`, push `a - b` back  
3. Return **remaining stone** or 0

---

## 💻 Code

```java
import java.util.PriorityQueue;
import java.util.Collections;

public class Solution {
    public static int weightOfLastStone(int arr[]) {

        // Max-Heap
        PriorityQueue<Integer> pq = new PriorityQueue<>(Collections.reverseOrder());

        // Insert all stones
        for (int stone : arr) {
            pq.add(stone);
        }

        // Smash until 0 or 1 stone left
        while (pq.size() > 1) {
            int a = pq.poll();  // largest
            int b = pq.poll();  // second largest

            if (a != b) {
                pq.add(a - b);
            }
        }

        return pq.isEmpty() ? 0 : pq.peek();
    }
}
```
---
### ⏱️ Time Complexity
- Heap operations: O(N log N)
### 📦 Space Complexity
- O(N) for the heap
