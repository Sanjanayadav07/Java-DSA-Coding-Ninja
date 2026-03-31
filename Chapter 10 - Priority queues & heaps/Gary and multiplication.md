# 🍬  Gary and multiplication

## 📌 Problem
👉 **Buy 1 candy → get K candies free**  
Find:
- 🔽 Minimum cost  
- 🔼 Maximum cost  

---

## 🧠 Key Idea (Math + Greedy)

- Instead of simulating skipping, we calculate:

- 👉 **How many candies we actually need to BUY**

---

## 🎯 Formula

- Buy count = ceil(n / (k + 1))
- 👉 Because:
- 1 buy + k free = (k + 1) candies covered

---

## 🛠️ Approach

### 🔹 Step 1: Sort array

- Arrays.sort(cost)
---

## 🔽 Minimum Cost
- 👉 Buy **smallest elements**
- sum first 'number' elements


---

## 🔼 Maximum Cost

👉 Buy **largest elements**
- sum last 'number' elements

---

## 💻 Code

```java
import java.util.*;

public class Solution {

    // Minimum cost
    public static int minimumCost(int[] cost, int n, int k) {
        Arrays.sort(cost);

        k = k + 1;  
        int number = (int) Math.ceil((double) n / k);

        int sum = 0;
        for (int i = 0; i < number; i++) {
            sum += cost[i];
        }

        return sum;
    }

    // Maximum cost
    public static int maximumCost(int[] cost, int n, int k) {
        Arrays.sort(cost);

        k = k + 1;
        int number = (int) Math.ceil((double) n / k);

        int sum = 0;
        for (int i = n - 1; i >= n - number; i--) {
            sum += cost[i];
        }

        return sum;
    }
}
```
---
### ⏱️ Time Complexity
- O(N log N)
- Sorting dominates

### 📦 Space Complexity
- O(1)
