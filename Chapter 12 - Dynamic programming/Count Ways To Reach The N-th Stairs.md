# Count Distinct Ways to Climb Stairs

## 📌 Problem
You can climb 1 or 2 steps at a time.
Find number of ways to reach n-th stair.

---

## 🧠 Approach
This is a Fibonacci-style DP problem:

dp[n] = dp[n-1] + dp[n-2]

---

## 🔥 Base Cases
- dp[0] = 1
- dp[1] = 1

---

## Code 
```
import java.util.* ;
import java.io.*; 
public class Solution {
	public static long countDistinctWayToClimbStair(int nStairs) {
		// Write your code here.
        if(nStairs<=1) return 1;
        int mod=1000000007;
        int prev=1;// o stairs
        int prev2=1;// 1 stairs
        for(int i=2;i<=nStairs;i++){
            int curr=(prev+prev2)%mod;
            prev2=prev;
            prev=curr;
        }
        return prev;
	}
}
```
---

## ⚡ Complexity
- Time: O(N)
- Space: O(1)
