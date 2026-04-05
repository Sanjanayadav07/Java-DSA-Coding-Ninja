# 🔤 Transformed String (Using Min Heap)

## 📌 Problem
Given a string `str` and integer `k`,  
we need to create a **new lexicographically smallest string** using a sliding window of size `k`.

---

## 🧠 Key Idea

👉 Use **Min Heap (PriorityQueue)**  
👉 Maintain a window of size `k`  
👉 Always pick the **smallest character** first  

---

## 🛠️ Approach

1. Add first `k` characters into min heap  
2. For remaining characters:
   - Remove smallest from heap → add to result  
   - Add next character to heap  
3. At end → empty heap into result  

---

## 💻 Code

```java
import java.util.PriorityQueue;

public class Solution {

    public static String getTransformedString(String str, int k) {

        PriorityQueue<Character> pq = new PriorityQueue<>();
        StringBuilder ans = new StringBuilder();

        for (int i = 0; i < str.length(); i++) {

            if (i < k) {
                pq.add(str.charAt(i));
            } else {
                ans.append(pq.poll());   // smallest character
                pq.add(str.charAt(i));
            }
        }

        // Add remaining characters
        while (!pq.isEmpty()) {
            ans.append(pq.poll());
        }

        return ans.toString();
    }
}
```
---
### ⏱️ Time Complexity
- O(N log K)
- Each insertion/removal → log K
- Total operations → N
### 📦 Space Complexity
- O(K)
- Heap stores at most K elements
