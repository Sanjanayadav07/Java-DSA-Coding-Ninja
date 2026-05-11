# Optimal Game Strategy (Coins Game)

## 📌 Problem
Two players pick coins from either end of an array.
Each plays optimally.

Find maximum coins first player can collect.

---

## 🧠 Approach
Use Dynamic Programming (Interval DP):

- dp[i][j] → max coins from i to j
- Player picks left or right
- Opponent minimizes your future gain

---

## 🔁 Transition
If pick left:
→ coins[i] + min(opponent options)

If pick right:
→ coins[j] + min(opponent options)

---
## Code 
```
import java.util.* ;
import java.io.*; 
import java.util.*;

public class Solution {

    public static int maxCoins(int[] coins, int numberOfCoins) {

        int n = coins.length;

        int[][] dp = new int[n][n];

        // d = gap between i and j
        for (int d = 0; d < n; d++) {

            for (int i = 0, j = d; j < n; i++, j++) {

                // Only one coin
                if (d == 0) {
                    dp[i][j] = coins[i];
                }

                // Two coins
                else if (d == 1) {
                    dp[i][j] = Math.max(coins[i], coins[j]);
                }

                else {

                    // If player picks first coin
                    int val1 = coins[i] +
                            Math.min(dp[i + 2][j], dp[i + 1][j - 1]);

                    // If player picks last coin
                    int val2 = coins[j] +
                            Math.min(dp[i][j - 2], dp[i + 1][j - 1]);

                    // Store maximum profit
                    dp[i][j] = Math.max(val1, val2);
                }
            }
        }

        return dp[0][n - 1];
    }
}
```
---

## ⚡ Complexity
- Time: O(N²)
- Space: O(N²)
