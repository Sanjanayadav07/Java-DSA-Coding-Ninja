# Optimal Strategy For A Game

## 📌 Problem

Two players are playing a game.

They can pick a coin only from:
- Left End
- Right End

Both players play optimally.

Find the maximum amount of money the first player can collect.

---

## 🧠 Key Idea

At every step:

Player has two choices:

1. Pick Left Coin
2. Pick Right Coin

Opponent also plays optimally and tries to minimize our future profit.

Therefore we use:

min()

for opponent's move.

---

## 🔥 DP State

dp[i][j]

Maximum amount obtainable from coins between i and j.

---

## Transition

Pick Left:

coins[i] +
min(
    dp[i+2][j],
    dp[i+1][j-1]
)

Pick Right:

coins[j] +
min(
    dp[i][j-2],
    dp[i+1][j-1]
)

Answer:

max(left, right)

---
## Code 
```
import java.util.* ;
import java.io.*; 
public class Solution {
    public static int optimalStrategyOfGame(int[] coins, int n) {
        // Write your code here. 
        int[][] dp = new int[n][n];
        for (int[] row : dp) Arrays.fill(row, -1); 
        return rec(0, n - 1, coins, dp);  
    }
    public static int rec(int i, int j, int[] coins, int[][] dp) {
        if (i > j) return 0; 
        if (i == j) return coins[i]; 
        if (dp[i][j] != -1) return dp[i][j];
        int option1 = coins[i] + Math.min(rec(i + 2, j, coins, dp), rec(i + 1, j - 1, coins, dp));
        int option2 = coins[j] + Math.min(rec(i, j - 2, coins, dp), rec(i + 1, j - 1, coins, dp));
        dp[i][j] = Math.max(option1, option2);

        return dp[i][j];
    }
}

```
---

## ⏱️ Complexity

Time Complexity:
O(N²)

Space Complexity:
O(N²)
