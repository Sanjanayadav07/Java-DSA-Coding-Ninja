# Minimum Cost to Merge 

## 📌 Problem
Given an array, split it into segments.
Each merge cost = sum of elements in that segment.

Goal → minimize total cost.

---

## 🧠 Approach
- Use Interval DP
- Try all possible partitions
- Recursively compute left + right + current cost

---

## code 
```
import java.util.*;

public class Solution {

    static int[][] dp = new int[101][101];

    // Recursive function with memoization
    static int solve(int i, int j, int[] arr) {

        // Base case
        if (i >= j) return 0;

        // Already computed
        if (dp[i][j] != -1) return dp[i][j];

        int ans = Integer.MAX_VALUE;

        // Compute sum of current segment
        int sum = 0;
        for (int k = i; k <= j; k++) {
            sum += arr[k];
        }

        // Try all partitions
        for (int k = i + 1; k <= j; k++) {

            int cost = sum
                    + solve(i, k - 1, arr)
                    + solve(k, j, arr);

            ans = Math.min(ans, cost);
        }

        return dp[i][j] = ans;
    }

    public static int findMinCost(int[] arr, int n) {

        // Initialize DP
        for (int i = 0; i < 101; i++) {
            Arrays.fill(dp[i], -1);
        }

        return solve(0, n - 1, arr);
    }
}
```
---

## ⚡ Complexity
- Time: O(N^3)
- Space: O(N^2)
