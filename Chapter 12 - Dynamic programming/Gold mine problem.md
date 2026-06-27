# Problem Statement

Given a gold mine represented by an `N × M` grid, where each cell contains a certain amount of gold.

A miner can start from any row in the first column and move only in the following directions:

- Right `(i, j+1)`
- Right-Up `(i-1, j+1)`
- Right-Down `(i+1, j+1)`

Find the maximum amount of gold that can be collected.

---

# Approach

## Key Idea

Use Dynamic Programming.

Let:

dp[i][j] = Maximum gold that can be collected starting from cell `(i, j)` and moving towards the last column.

Since every state depends on the next column, we fill the DP table from right to left.

---

## DP Transition

From cell `(i, j)`, we have three possible moves:

1. Right
2. Right-Up
3. Right-Down

Therefore:

dp[i][j] = mine[i][j] +
            max(
                right,
                rightUp,
                rightDown
            )

where:

- right = dp[i][j+1]
- rightUp = dp[i-1][j+1]
- rightDown = dp[i+1][j+1]

Boundary conditions are handled appropriately.

---

## Base Case

For the last column:

dp[i][m-1] = mine[i][m-1]

because no further moves are possible.

---

# Code

```java
import java.util.*;

public class Solution {

    public static int maxGoldCollected(int[][] mine, int n, int m) {

        int ans = 0;
        int[][] dp = new int[n][m];

        for (int j = m - 1; j >= 0; j--) {

            for (int i = 0; i < n; i++) {

                int takeUp = (j == m - 1) ? 0 : dp[i][j + 1];

                int goStraight =
                        (i == 0 || j == m - 1)
                                ? 0
                                : dp[i - 1][j + 1];

                int takeDown =
                        (i == n - 1 || j == m - 1)
                                ? 0
                                : dp[i + 1][j + 1];

                dp[i][j] = mine[i][j]
                        + Math.max(
                                takeDown,
                                Math.max(takeUp, goStraight)
                        );
            }
        }

        for (int i = 0; i < n; i++) {
            ans = Math.max(ans, dp[i][0]);
        }

        return ans;
    }
}

```
---
### Time Complexity
- O(N × M)
- Each cell is processed exactly once.
### Space Complexity
- O(N × M)
- DP table of size N × M.
