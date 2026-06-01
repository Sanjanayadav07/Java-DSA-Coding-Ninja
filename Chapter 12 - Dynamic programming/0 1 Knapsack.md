# 0/1 Knapsack Problem

## 📌 Problem
Given:
- weights[]
- values[]
- bag capacity W

Find maximum profit.

Each item can be chosen only once.

---

## 🧠 Approach
Use Recursion + Memoization.

For every item:
- Take it
- Skip it

Store results in DP table.

---

## 🔥 DP State

dp[n][w] =
maximum profit using first n items
with capacity w

---
## Code
```
import java.util.ArrayList;
import java.util.Arrays;

public class Solution {

    static int[][] t;

    private static int solve(int n, int w,ArrayList<Integer> weights,ArrayList<Integer> values) {

        if (n == 0 || w == 0) return 0;

        if (t[n][w] != -1) return t[n][w];

        if (weights.get(n - 1) <= w) {

            int take = values.get(n - 1) + solve(n - 1,w - weights.get(n - 1),weights,values);

            int skip = solve(n - 1, w, weights, values);

            return t[n][w] = Math.max(take, skip);
        }

        return t[n][w] = solve(n - 1, w, weights, values);
    }

    public static int maxProfit(ArrayList<Integer> values,ArrayList<Integer> weights,int n,int w) {

        t = new int[n + 1][w + 1];

        for (int[] row : t) {
            Arrays.fill(row, -1);
        }

        return solve(n, w, weights, values);
    }
}
```
---

## ⚡ Complexity
- Time: O(N × W)
- Space: O(N × W)
___
