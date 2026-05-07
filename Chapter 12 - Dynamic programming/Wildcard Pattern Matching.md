# Wildcard Pattern Matching

## 📌 Problem
Match a string with a pattern containing:
- `?` → matches single character
- `*` → matches any sequence (including empty)

---

## 🧠 Approach
Use Dynamic Programming:

- `dp[i][j]` → whether `text[0..i]` matches `pattern[0..j]`
- Handle `?`, `*`, and normal characters separately

---

## ⚡ Transitions
- Match or `?` → `dp[i-1][j-1]`
- `*` → `dp[i][j-1] OR dp[i-1][j]`

---
## code 
```

public class Solution {

    public static boolean wildcardMatching(String pattern, String text) {

        int n = text.length();
        int m = pattern.length();

        boolean[][] dp = new boolean[n + 1][m + 1];

        // Empty pattern matches empty text
        dp[0][0] = true;

        // Handle patterns like *, **, *** with empty text
        for (int j = 1; j <= m; j++) {
            if (pattern.charAt(j - 1) == '*') {
                dp[0][j] = dp[0][j - 1];
            }
        }

        // Fill DP table
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {

                char t = text.charAt(i - 1);
                char p = pattern.charAt(j - 1);

                // Direct match or '?'
                if (p == t || p == '?') {
                    dp[i][j] = dp[i - 1][j - 1];
                }

                // '*' → empty OR one/more characters
                else if (p == '*') {
                    dp[i][j] = dp[i][j - 1] || dp[i - 1][j];
                }

                else {
                    dp[i][j] = false;
                }
            }
        }

        return dp[n][m];
    }
}
```
---

## ⚡ Complexity
- Time: O(N × M)
- Space: O(N × M)
