# Maximize The Cut Segments

## 📌 Problem
Given a rod of length `N`,
cut it into maximum number of segments
using only lengths:
- A
- B
- C

---

## 🧠 Approach
Use Dynamic Programming.

dp[i] =
maximum cuts possible for length i

---

## 🔥 Transition
Try all 3 cuts:
- i - A
- i - B
- i - C

Take maximum.

---
## Code
```
import java.util.* ;
import java.io.*; 

public class Solution 
{
	public static int findMaxNumSegements(int len, int scaleA,int scaleB,int scaleC) 
	{
		int[] dp = new int[len + 1];

		Arrays.fill(dp, -1);

		dp[0] = 0;

		for(int i = 1; i <= len; i++) {

			if(i - scaleA >= 0 && dp[i - scaleA] != -1) {
				dp[i] = Math.max(dp[i], dp[i - scaleA] + 1);
			}

			if(i - scaleB >= 0 && dp[i - scaleB] != -1) {
				dp[i] = Math.max(dp[i], dp[i - scaleB] + 1);
			}

			if(i - scaleC >= 0 && dp[i - scaleC] != -1) {
				dp[i] = Math.max(dp[i], dp[i - scaleC] + 1);
			}
		}

		return Math.max(dp[len], 0);
	}
}
```
---

## ⚡ Complexity
- Time: O(N)
- Space: O(N)
