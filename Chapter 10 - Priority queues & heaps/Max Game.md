# 🍬 Candy Store (Min & Max Cost)

## 📌 Problem
- 👉 Buy 1 candy → get K candies free  
- Find **minimum** and **maximum** cost

---

## 🧠 Approach (Greedy + Math)

- 👉 Total candies covered in one buy:

- k + 1


- 👉 Number of candies we need to BUY:

- ceil(n / (k + 1))


---

## 💻 Code

```java
import java.util.*;

public class Solution {

    public static int minimumCost(int[] cost, int n, int k) {
        Arrays.sort(cost);

        int buy = (int)Math.ceil((double)n / (k + 1));

        int sum = 0;
        for (int i = 0; i < buy; i++) {
            sum += cost[i];   // smallest
        }

        return sum;
    }

    public static int maximumCost(int[] cost, int n, int k) {
        Arrays.sort(cost);

        int buy = (int)Math.ceil((double)n / (k + 1));

        int sum = 0;
        for (int i = n - 1; i >= n - buy; i--) {
            sum += cost[i];   // largest
        }

        return sum;
    }
}
```
---
### ⏱️ Time Complexity
- O(N log N)
### 📦 Space Complexity
- O(1)
