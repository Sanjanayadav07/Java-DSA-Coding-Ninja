# Longest Increasing Subsequence (LIS)

## 📌 Problem
Find the length of the longest strictly increasing subsequence.

---

## 🧠 Approach
Use:
- Greedy
- Binary Search

Maintain a list:
- Replace element using binary search
- Keep list sorted

---

## 🔥 Key Idea
The list does NOT store actual LIS.
It stores optimal subsequence endings.

---
## Code
```
import java.util.*;

public class Solution {

    public static int longestIncreasingSubsequence(int[] arr) {

        int n = arr.length;

        if (n == 0) {
            return 0;
        }

        ArrayList<Integer> list = new ArrayList<>();

        for (int num : arr) {

            int idx = Collections.binarySearch(list, num);

            // If not found
            if (idx < 0) {
                idx = -(idx + 1);
            }

            // Replace or add
            if (idx == list.size()) {
                list.add(num);
            } else {
                list.set(idx, num);
            }
        }

        return list.size();
    }
}
```
---

## ⚡ Complexity
- Time: O(N log N)
- Space: O(N)
