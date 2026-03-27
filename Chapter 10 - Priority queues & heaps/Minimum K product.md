# 🔽 Minimum Product of K Numbers

## 📌 Problem
Given an array, find the **minimum product of K elements**.

- 👉 Return result modulo: 10^9 + 7

---

## 🧠 Key Idea

- To get **minimum product**:
- 👉 Choose the **K smallest elements**
- ✔ Use **Min Heap** to efficiently extract smallest values

---

## 🛠️ Approach

### Step 1: Build Min Heap

- PriorityQueue<Integer> pq = new PriorityQueue<>();
- 👉 Insert all elements

---

### Step 2: Extract K smallest elements
- for k times:
- product *= pq.poll()
---

### Step 3: Use Modulo
- product = (product * value) % MOD
- 👉 Prevents overflow

---

## 💻 Code

```java
import java.util.*;

public class Solution {

    public static final int MOD = (int)1e9 + 7;

    public static int minProduct(int[] arr, int n, int k) {

        PriorityQueue<Integer> pq = new PriorityQueue<>();

        // Insert all elements
        for (int i = 0; i < n; i++) {
            pq.add(arr[i]);
        }

        long product = 1;

        // Take k smallest elements
        for (int i = 0; i < k; i++) {
            product = (product * pq.poll()) % MOD;
        }

        return (int) product;
    }
}
```
---
### ⏱️ Time Complexity
- O(N log N)
- Heap insertion → O(N log N)
- K removals → O(K log N)
### 📦 Space Complexity
- O(N)
- Heap stores all elements
