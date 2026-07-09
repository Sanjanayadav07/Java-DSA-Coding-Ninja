# Problem Statement

A person wants to cover a distance of `n` units.

At each move, the person can jump:

- 1 unit
- 2 units
- 3 units

Find the total number of distinct ways to reach exactly distance `n`.

Since the answer can be very large, return it modulo `10^9 + 7`.

---

# Approach

## Key Idea

To reach distance `i`, the last jump can be:

- 1 unit (coming from `i-1`)
- 2 units (coming from `i-2`)
- 3 units (coming from `i-3`)

Therefore, the total ways to reach `i` are the sum of ways to reach these previous positions.

---

## DP State

Let:

dp[i] = Number of ways to reach distance i

---

## Recurrence

dp[i] = dp[i-1] + dp[i-2] + dp[i-3]

Apply modulo `10^9 + 7` after every operation.

---

## Base Case

dp[0] = 1

There is exactly one way to cover distance 0: do nothing.

---

## Code

```java
import java.util.*;

public class Solution {

    public static int distance(int n) {
        long MOD = 1000000007L;

        long[] dp = new long[n + 1];
        dp[0] = 1;

        for (int i = 1; i <= n; i++) {
            dp[i] = dp[i - 1] % MOD;

            if (i >= 2) {
                dp[i] = (dp[i] + dp[i - 2]) % MOD;
            }

            if (i >= 3) {
                dp[i] = (dp[i] + dp[i - 3]) % MOD;
            }
        }

        return (int) dp[n];
    }
}
```
---
### Time Complexity
- O(n)
- We compute each DP state exactly once.
### Space Complexity
- O(n)
- DP array of size n + 1 is used.
---
