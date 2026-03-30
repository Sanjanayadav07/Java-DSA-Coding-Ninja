# 🍬 Candy Store Problem (Min & Max Cost)

## 📌 Problem
Given cost of candies and offer:

👉 **Buy 1 candy → get K candies free**

Find:
- 💰 **Minimum cost**
- 💰 **Maximum cost**

---

## 🧠 Key Idea (Greedy)

### 🔽 Minimum Cost
👉 Buy **cheapest candy**  
👉 Get **K most expensive free**

---

### 🔼 Maximum Cost
👉 Buy **most expensive candy**  
👉 Get **K cheapest free**

---

## 🛠️ Approach

### 🔹 Step 1: Sort array

- Arrays.sort(cost)

---

## 🔽 Minimum Cost Logic
- i = 0 (cheapest)
- j = n-1 (expensive)

- while(i <= j):
- buy cost[i]
- i++
- j = j - k // skip k expensive


---

## 🔼 Maximum Cost Logic
- i = 0 (cheapest)
- j = n-1 (expensive)

- while(i <= j):
- buy cost[j]
- j--
- i = i + k // skip k cheapest

---

## 💻  Code

```java
import java.util.*;

public class Solution {

    // Minimum cost
    public static long minimumCost(int[] cost, int n, int k) {
        Arrays.sort(cost);

        long ans = 0;
        int i = 0, j = n - 1;

        while (i <= j) {
            ans += cost[i++];   // buy cheapest
            j = j - k;          // skip k expensive
        }

        return ans;
    }

    // Maximum cost
    public static long maximumCost(int[] cost, int n, int k) {
        Arrays.sort(cost);

        long ans = 0;
        int i = 0, j = n - 1;

        while (i <= j) {
            ans += cost[j--];   // buy expensive
            i = i + k;          // skip k cheapest
        }

        return ans;
    }
}
```
---
### ⏱️ Time Complexity
- O(N log N)
- Sorting dominates
### 📦 Space Complexity
- O(1)
- No extra space used
