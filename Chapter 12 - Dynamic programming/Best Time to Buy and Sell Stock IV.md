# Stock Buy and Sell - K Transactions

## 📌 Problem
You are given stock prices and can perform at most K transactions.
Find maximum profit.

---

## 🧠 Approach
Use Dynamic Programming:

States:
- `cap` → remaining transactions
- `buy` → 1 (buy allowed), 0 (sell allowed)

---

## 🔁 Transitions
- Buy → `-price + next_sell_state`
- Sell → `+price + next_buy_state`

---
## Code 
```
import java.util.*;

public class Solution {

    public static int maximumProfit(int[] prices, int n, int k) {

        // dp[cap][buy]
        // cap = remaining transactions
        // buy = 1 (can buy), 0 (must sell)
        int[][] dp = new int[k + 1][2];

        // Traverse from last day to first day
        for (int i = n - 1; i >= 0; i--) {

            int[][] curr = new int[k + 1][2];

            for (int cap = 1; cap <= k; cap++) {

                // BUY state
                curr[cap][1] = Math.max(
                    -prices[i] + dp[cap][0],  // buy stock
                    dp[cap][1]                // skip
                );

                // SELL state
                curr[cap][0] = Math.max(
                    prices[i] + dp[cap - 1][1], // sell stock
                    dp[cap][0]                 // skip
                );
            }

            dp = curr;
        }

        return dp[k][1]; // start with full capacity, allowed to buy
    }
}
```

---

## ⚡ Complexity
- Time: O(N × K)
- Space: O(K)
