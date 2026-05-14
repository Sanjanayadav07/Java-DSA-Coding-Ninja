# Count Balanced Binary Trees

## 📌 Problem
Count the number of balanced binary trees of height `n`.

Return answer modulo `10^9 + 7`.

---

## 🧠 Approach
For a balanced tree of height `h`:

Possible subtree heights:
- (h-1, h-1)
- (h-1, h-2)
- (h-2, h-1)

---

## 🔥 Recurrence

dp[h] =
dp[h-1]^2 + 2 * dp[h-1] * dp[h-2]

---
## Code 

```
import java.util.* ;
import java.io.*; 

public class Solution 
{
    public static int countBalancedBinaryTree(int n)
    {
        long mod = 1000000007;

        long dp[] = new long[n + 1];

        dp[0] = 1;
        dp[1] = 1;

        for(int i = 2; i <= n; i++) 
        {
            dp[i] = (dp[i - 1] * 
                    ((2 * dp[i - 2]) % mod + dp[i - 1]) % mod) % mod;
        }

        return (int)dp[n];
    }
}
```

---

## ⚡ Complexity
- Time: O(N)
- Space: O(N)
