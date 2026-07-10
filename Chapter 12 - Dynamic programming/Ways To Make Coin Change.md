# Coin Change 2 (Count Ways To Make Change)

## 📌 Problem
Given coin denominations and target value,
count total ways to make the value.

Unlimited usage of coins allowed.

---

## 🧠 Approach
Use Recursion + Memoization.

At every coin:
- Take current coin
- Skip current coin

Add both answers.

---

## 🔥 DP State

dp[i][value] =
number of ways using coins from i onward

---
## Code 
```
import java.util.*;

public class Solution {

    static long[][] dp;
    static int n;

    private static long solve(int[] denominations, int i, int value) {

        // Base cases
        if (value == 0) return 1;

        if (i == n || value < 0) return 0;

        // Memoization check
        if (dp[i][value] != -1) {
            return dp[i][value];
        }

        // If current coin is greater than remaining value
        if (denominations[i] > value) {
            return dp[i][value] = solve(denominations, i + 1, value);
        }

        // Take current coin
        long take = solve(denominations, i, value - denominations[i]);

        // Skip current coin
        long skip = solve(denominations, i + 1, value);

        return dp[i][value] = take + skip;
    }

    public static long countWaysToMakeChange(int denominations[], int value) {

        n = denominations.length;

        dp = new long[n][value + 1];

        for (long[] row : dp) {
            Arrays.fill(row, -1);
        }

        return solve(denominations, 0, value);
    }
}
```
---

## ⚡ Complexity
- Time: O(N × VALUE)
- Space: O(N × VALUE)
---
