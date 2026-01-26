# 🔢 Count Occurrences of an Element in Sorted Array 

Count the total number of occurrences of a given element `x` in a **sorted array** using **binary search**.

---

## 📌 Problem Statement

Given a sorted array `arr[]` of size `n` and an integer `x`, find how many times `x` appears in the array.

- If `x` is not present, return `0`
- The solution should be efficient

---
## ⏱️ Time & Space Complexity

 - Time Complexity: O(log n)
    - Two binary searches
 - Space Complexity: O(1)
    - Constant extra space
---

## 🧠 Approach

- Use **binary search twice**:
  - First to find the **first occurrence** of `x`
  - Second to find the **last occurrence** of `x`
- If `x` is not found, return `0`
- Otherwise, count = `last - first + 1`

---

## 💻 Code 

```java
public class Solution {

    public static int count(int arr[], int n, int x) {

        // Find first occurrence
        int left = 0, right = n - 1;
        int first = -1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (arr[mid] == x) {
                first = mid;
                right = mid - 1;
            } else if (arr[mid] < x) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        if (first == -1) return 0; // x not found

        // Find last occurrence
        left = 0;
        right = n - 1;
        int last = -1;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (arr[mid] == x) {
                last = mid;
                left = mid + 1;
            } else if (arr[mid] < x) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        return last - first + 1;
    }
}
