## 📌 Problem Statement

- Given an array arr of size n and an integer k, you can remove elements from the array.
-  Your goal is to minimize the number of removals such that the difference between the maximum and minimum elements of the remaining array is at most k.
- In other words, after removals:
   - max(remaining) - min(remaining) ≤ k
- Return the minimum number of removals required.
---
## 💡 Approach
### 🔑 Key Idea:
- We want the largest possible subset where:
   - arr[max] - arr[min] ≤ k
- So instead of removing elements directly, we:
  - Sort the array
- Use a sliding window (two pointers) to find the largest valid subarray
- Answer = n - size_of_largest_valid_window
---
## 🪜 Steps:
- Sort the array
- Use two pointers:
   - low → start of window
   - high → expand window
- If condition holds:
  - arr[high] - arr[low] ≤ k
- → update max window size
- Else:
 - → move low forward
- Finally:
- answer = n - max_window_size
---
## 🧾 Code
```
import java.util.* ;
import java.io.*; 
import java.util.ArrayList;

public class Solution 
{
    public static int minimumRemovals(ArrayList<Integer> arr, int n, int k)
    {
        Collections.sort(arr);

        int low = 0;
        int high = 1;
        int ans = 0;

        while (high < n) {
            if (arr.get(high) - arr.get(low) <= k) {
                ans = Math.max(ans, high - low + 1);
                high++;
            } else {
                low++;
            }
        }

        if (ans <= 0) return 0;
        return n - ans;
    }
}
```
---
## ⏱️ Time Complexity
- O(n log n)
- Sorting takes O(n log n)
- Two pointer traversal takes O(n)
### 🧠 Space Complexity
- O(1)
- No extra space used (ignoring sorting internals)
