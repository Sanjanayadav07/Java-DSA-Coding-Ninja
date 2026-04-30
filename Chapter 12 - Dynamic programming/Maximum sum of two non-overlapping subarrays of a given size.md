# 📌 Maximum Sum of Two Non-Overlapping Subarrays (Size K)
## 🧾 Problem Statement

- Given an integer array arr of size N and an integer K, find the maximum sum of two non-overlapping subarrays, each of size K.

- Both subarrays must be contiguous.
- They must not overlap.
---
## 💡 Approach

- We use Dynamic Programming + Sliding Window.

### 🔹 Step 1: Left to Right (dp1[])
- dp1[i] stores the maximum sum of any subarray of size K from index 0 to i
- Use a sliding window to maintain sum of last K elements

- At each step:

- dp1[i] = max(current_window_sum, dp1[i-1])
---
### 🔹 Step 2: Right to Left (dp2[])
- dp2[i] stores the maximum sum of any subarray of size K from index i to N-1
- Traverse from right and apply reverse sliding window

- At each step:

- dp2[i] = max(current_window_sum, dp2[i+1])
---
### 🔹 Step 3: Combine Results
- Try every valid split point i
- Left subarray ends at i
- Right subarray starts at i + 1
- ans = max(dp1[i] + dp2[i+1])
---
## ✅ Code
```
import java.util.*;
import java.io.*;

public class Solution {

    public static int maxSumTwoSubarray(int[] arr, int N, int K) {

        int dp1[] = new int[N]; // left max
        int dp2[] = new int[N]; // right max

        int sum = 0;

        // LEFT TO RIGHT
        for (int i = 0; i < N; i++) {
            if (i < K) {
                sum += arr[i];
                dp1[i] = sum;
            } else {
                sum += arr[i] - arr[i - K];
                dp1[i] = Math.max(sum, dp1[i - 1]);
            }
        }

        sum = 0;

        // RIGHT TO LEFT
        for (int i = N - 1; i >= 0; i--) {
            if (i + K >= N) {
                sum += arr[i];
                dp2[i] = sum;
            } else {
                sum += arr[i] - arr[i + K];
                dp2[i] = Math.max(sum, dp2[i + 1]);
            }
        }

        int ans = Integer.MIN_VALUE;

        // COMBINE
        for (int i = K - 1; i < N - K; i++) {
            ans = Math.max(ans, dp1[i] + dp2[i + 1]);
        }

        return ans;
    }
}
```
---
### ⏱ Time Complexity
- O(N)
- (Single pass for dp1, dp2, and final loop)
### 💾 Space Complexity
- O(N)
- (Two auxiliary arrays: dp1 and dp2)
