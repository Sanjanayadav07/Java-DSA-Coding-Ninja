## 📌 Problem Statement

- Given three strings A, B, and C, find the length of the Longest Common Subsequence (LCS) present in all three strings.

- A subsequence is a sequence that appears in the same relative order, but not necessarily contiguous.
---
## 💡 Approach
### 🔑 Key Idea:

- This is a 3D Dynamic Programming (DP) extension of the classic LCS problem.

- We define:

- dp[i][j][k] = LCS length of
- A[i...], B[j...], C[k...]
---
## 🪜 Recurrence:
- If characters match:
- A[i] == B[j] == C[k]
- Then:
- dp[i][j][k] = 1 + dp[i+1][j+1][k+1]
-  If not equal:
- We skip one character from any of the strings:
```
dp[i][j][k] = max(
    dp[i+1][j][k],
    dp[i][j+1][k],
    dp[i][j][k+1]
)
```
- 🧠 Bottom-Up Strategy:
- We fill the DP table from back to front so that future states are already computed.
----
## 🧾 Code 
```
import java.util.*;

public class Solution {

    public static int LCS(String A, String B, String C, int n, int m, int k) {

        int[][][] dp = new int[n + 1][m + 1][k + 1];

        for (int i = n - 1; i >= 0; i--) {
            for (int j = m - 1; j >= 0; j--) {
                for (int l = k - 1; l >= 0; l--) {

                    if (A.charAt(i) == B.charAt(j) && B.charAt(j) == C.charAt(l)) {
                        dp[i][j][l] = 1 + dp[i + 1][j + 1][l + 1];
                    } else {
                        dp[i][j][l] = Math.max(
                            dp[i + 1][j][l],
                            Math.max(
                                dp[i][j + 1][l],
                                dp[i][j][l + 1]
                            )
                        );
                    }
                }
            }
        }

        return dp[0][0][0];
    }
}
```
---
### ⏱️ Time Complexity
- O(n × m × k)
- We fill each DP state once.

### 🧠 Space Complexity
- O(n × m × k)
- For the 3D DP table.
