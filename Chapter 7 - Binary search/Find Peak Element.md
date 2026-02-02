# 🏔️ Find Peak Element 

## 📌 Problem Statement
Given an array `arr` of integers, find the **index of any peak element**.

A **peak element** is an element that is **strictly greater than its neighbors**.

> You may assume that:
> - `arr[-1] = arr[n] = -∞`
> - There is always at least one peak element.

---

## 💡 Approach (Binary Search – Divide & Conquer)

1. Use **Binary Search** instead of linear scan.
2. Find middle element:
   - If `arr[mid] > arr[mid + 1]` → peak lies on the **left side**
   - Else → peak lies on the **right side**
3. Continue until `low == high`
4. That index is the **peak element**

This works because at least one peak always exists.

---
⏱️ Time Complexity 
  - Time Complexity=O(logN)
	​
## 🧠 Space Complexity 
  - Space Complexity=O(logN)
---

## 🧠 Code

```java
import java.util.ArrayList;

public class Solution {

    // Helper function using Binary Search
    public static int isPeak(ArrayList<Integer> arr, int l, int h) {
        if (l == h) {
            return l;
        }

        int mid = l + (h - l) / 2;

        if (arr.get(mid) > arr.get(mid + 1)) {
            return isPeak(arr, l, mid);
        } else {
            return isPeak(arr, mid + 1, h);
        }
    }

    // Main function
    public static int findPeakElement(ArrayList<Integer> arr) {
        return isPeak(arr, 0, arr.size() - 1);
    }
}
