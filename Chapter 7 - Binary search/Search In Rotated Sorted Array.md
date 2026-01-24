# 🔍 Search in Rotated Sorted Array 

Search an element in a rotated sorted array using modified binary search.

---

## 📌 Problem Statement

Given an `ArrayList<Integer>` that is sorted and then rotated, find the index of element `k`.

- Return index if found  
- Return `-1` if not found  
- Time Complexity: `O(log n)`

---
## ⏱️ Complexity

- Time: O(log n)
- Space: O(1)
---

## 🧠 Approach

- Use binary search
- Identify which half is sorted
- Narrow down search space accordingly

---

## 💻 Code

```java
import java.util.ArrayList;

public class Solution {
    public static int search(ArrayList<Integer> arr, int n, int k) {
        int low = 0, high = n - 1;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (arr.get(mid) == k)
                return mid;

            if (arr.get(low) <= arr.get(mid)) {
                if (arr.get(low) <= k && k < arr.get(mid)) {
                    high = mid - 1;
                } else {
                    low = mid + 1;
                }
            } else {
                if (arr.get(mid) < k && k <= arr.get(high)) {
                    low = mid + 1;
                } else {
                    high = mid - 1;
                }
            }
        }
        return -1;
    }
}
