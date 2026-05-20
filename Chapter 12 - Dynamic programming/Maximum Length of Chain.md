# Maximum Length Chain of Pairs

## 📌 Problem
Given pairs of numbers,
find the longest chain such that:

pair[i][1] < pair[j][0]

---

## 🧠 Approach
This problem is similar to Longest Increasing Subsequence (LIS).

### Steps:
1. Sort pairs by first element
2. Apply LIS logic

---

## 🔥 DP State

dp[i] =
maximum chain length ending at i

---
## Code 
```


import java.util.* ;
import java.io.*; 
import java.util.ArrayList;

public class Solution 
{
    public static int getLongestChainLength(ArrayList<ArrayList<Integer>> pairs)
    {
        int n = pairs.size();

        // Sort pairs according to first element
        Collections.sort(pairs, (a, b) -> a.get(0) - b.get(0));

        int[] t = new int[n];
        Arrays.fill(t, 1);

        int maxLIS = 1;

        for(int i = 1; i < n; i++) {

            for(int j = 0; j < i; j++) {

                // pair[j][1] < pair[i][0]
                if(pairs.get(j).get(1) < pairs.get(i).get(0)) {

                    t[i] = Math.max(t[i], t[j] + 1);
                }
            }

            maxLIS = Math.max(maxLIS, t[i]);
        }

        return maxLIS;
    }
}
```
---

## ⚡ Complexity
- Time: O(N²)
- Space: O(N)
