# Palindrome Partitioning - Minimum Cuts

## 📌 Problem
Given a string, partition it such that every substring is a palindrome.

Find minimum number of cuts required.

---

## 🧠 Approach
Two-step Dynamic Programming:

### Step 1:
Precompute palindrome table P[i][j]

### Step 2:
Use DP:
- dp[i] = minimum cuts for substring [0..i]

---

## 🔥 Transition
If s[j+1..i] is palindrome:
→ dp[i] = min(dp[i], dp[j] + 1)

---
## Code 
```
import java.util.*;

public class Solution {

    public static int palindromePartitioning(String str) {
        int n = str.length();
        if (n <= 1) return 0;

        // P[i][j] = true if substring i..j is palindrome
        boolean[][] P = new boolean[n][n];

        // 1. Fill palindrome table
        for (int i = 0; i < n; i++) {
            P[i][i] = true;
        }

        for (int L = 2; L <= n; L++) {
            for (int i = 0; i <= n - L; i++) {
                int j = i + L - 1;

                if (str.charAt(i) == str.charAt(j)) {
                    if (L == 2) {
                        P[i][j] = true;
                    } else {
                        P[i][j] = P[i + 1][j - 1];
                    }
                }
            }
        }

        // 2. DP for minimum cuts
        int[] dp = new int[n];

        for (int i = 0; i < n; i++) {
            if (P[0][i]) {
                dp[i] = 0;
            } else {
                dp[i] = Integer.MAX_VALUE;

                for (int j = 0; j < i; j++) {
                    if (P[j + 1][i]) {
                        dp[i] = Math.min(dp[i], dp[j] + 1);
                    }
                }
            }
        }

        return dp[n - 1];
    }
}

```
---

## ⚡ Complexity
- Time: O(N²)
- Space: O(N²)
