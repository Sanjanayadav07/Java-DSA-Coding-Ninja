# 🔍 First and Last Position of an Element in Sorted Array (Java)

Find the **first and last occurrence** of a given element `k` in a **sorted array** using **binary search**.

---

## 📌 Problem Statement

Given a sorted `ArrayList<Integer>` of size `n` and an integer `k`, find:

- The **first position** of `k`
- The **last position** of `k`

If `k` does not exist, return `[-1, -1]`.

---
## ⏱️ Time & Space Complexity
 - Time Complexity: O(log n)
    - Binary search is applied twice
 - Space Complexity: O(1)
   - No extra space used (constant space)
---
## 🧠 Approach

- Apply **binary search twice**:
  - First search → find **first occurrence**
  - Second search → find **last occurrence**
- When `k` is found:
  - Move **left** to get first position
  - Move **right** to get last position

---

## 💻 Code 

```java
import java.util.ArrayList;

public class Solution {

    private static int findFirstPosition(ArrayList<Integer> arr, int n, int k) {
        int l = 0, r = n - 1;
        int result = -1;

        while (l <= r) {
            int mid = l + (r - l) / 2;

            if (arr.get(mid) == k) {
                result = mid;
                r = mid - 1;
            } else if (arr.get(mid) > k) {
                r = mid - 1;
            } else {
                l = mid + 1;
            }
        }
        return result;
    }

    private static int findLastPosition(ArrayList<Integer> arr, int n, int k) {
        int l = 0, r = n - 1;
        int result = -1;

        while (l <= r) {
            int mid = l + (r - l) / 2;

            if (arr.get(mid) == k) {
                result = mid;
                l = mid + 1;
            } else if (arr.get(mid) > k) {
                r = mid - 1;
            } else {
                l = mid + 1;
            }
        }
        return result;
    }

    public static int[] firstAndLastPosition(ArrayList<Integer> arr, int n, int k) {
        int first = findFirstPosition(arr, n, k);
        int last = findLastPosition(arr, n, k);
        return new int[] { first, last };
    }
}
