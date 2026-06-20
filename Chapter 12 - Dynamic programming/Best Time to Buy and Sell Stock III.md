## 📌 Problem Statement

 - Given an array prices where prices[i] represents the stock price on the i-th day, find the maximum profit you can earn by performing at most 2 transactions.
---
## ✅ Rules:
- You must sell before buying again
- At most 2 complete transactions allowed
- One transaction = Buy + Sell
---
## 💡 Approach
### 🔑 Key Idea:

- This is a Dynamic Programming (State Machine) problem.

- We track transactions using states:

- Transaction State	Meaning0	
  - First Buy
  - 1	First Sell
  - 2	Second Buy
  - 3	Second Sell
---
## 🧠 Observation:
- Even transaction index → BUY state
- Odd transaction index → SELL state

- At every day:

  - BUY → either buy stock or skip
  - SELL → either sell stock or skip
---
## 🪜 DP Transition
- ✅ BUY State:
  - max(-price + nextState, skip)
- ✅ SELL State:
  - max(price + nextState, skip)
---
## 🧾 Code 
```
import java.util.*;

public class Solution {

    public static int maxProfit(ArrayList<Integer> prices, int n) {

        int[] curr = new int[5];

        for (int i = n - 1; i >= 0; i--) {

            for (int txn = 3; txn >= 0; txn--) {

                int profit = 0;

                if (txn % 2 == 0) {

                    // BUY state
                    profit = Math.max(
                            -prices.get(i) + curr[txn + 1],
                            curr[txn]
                    );

                } else {

                    // SELL state
                    profit = Math.max(
                            prices.get(i) + curr[txn + 1],
                            curr[txn]
                    );
                }

                curr[txn] = profit;
            }
        }

        return curr[0];
    }
}
```

---
## 📖 State Flow
- txn = 0 → First Buy
- txn = 1 → First Sell
- txn = 2 → Second Buy
- txn = 3 → Second Sell

- After transaction 4, no more operations allowed.
---
### ⏱️ Time Complexity
- O(n × 4) = O(n)

- Only 4 transaction states processed for each day.

### 🧠 Space Complexity
- O(1)

- Using only one array of fixed size.
