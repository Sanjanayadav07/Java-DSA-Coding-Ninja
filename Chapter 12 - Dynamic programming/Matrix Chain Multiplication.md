# Matrix Chain Multiplication (MCM)

## 📌 Problem
Given dimensions of matrices,
find minimum multiplication operations needed
to multiply all matrices.

---

## 🧠 Approach
Use Interval Dynamic Programming.

- Try every partition point
- Compute:
    left cost + right cost + multiplication cost

Take minimum among all partitions.

---

## ⚡ DP State
dp[i][j] =
minimum cost to multiply matrices from i to j

---
## code
```

import java.util.* ;
import java.io.*; 

public class Solution 
{
    public static int minMultiplicationOperations(ArrayList<Integer> arr)
    {
        int n = arr.size();

        // dp[i][j] = min cost to multiply matrices from i to j
        int[][] dp = new int[n][n];

        // gap (chain length)
        for (int len = 2; len < n; len++) {

            for (int i = 0; i < n - len; i++) {

                int j = i + len;

                dp[i][j] = Integer.MAX_VALUE;

                for (int k = i + 1; k < j; k++) {

                    int cost = dp[i][k] + dp[k][j]
                             + arr.get(i) * arr.get(k) * arr.get(j);

                    dp[i][j] = Math.min(dp[i][j], cost);
                }
            }
        }

        return dp[0][n - 1];
    }
}
```
---

## ⚡ Complexity
- Time: O(N^3)
- Space: O(N^2)
