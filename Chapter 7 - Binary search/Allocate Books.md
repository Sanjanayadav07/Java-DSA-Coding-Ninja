# 📚 Allocate Minimum Number of Pages 

Allocate books among students such that the **maximum number of pages assigned to any student is minimized**.

---

## 📌 Problem Statement

Given an array `arr` where each element represents the number of pages in a book, and an integer `m` representing the number of students:

- Each book must be allocated to **exactly one student**
- Each student must be allocated **contiguous books**
- Every student should get **at least one book**

Return the **minimum possible maximum pages** assigned to a student.  
If allocation is not possible, return `-1`.

---
## ⏱️ Time & Space Complexity

- Time Complexity: O(n × log(sum))
   - Binary search on answer range
   - isValid() runs in O(n)
- Space Complexity: O(1)
   - Constant extra space
---

## 🧠 Approach (Binary Search on Answer)

- The minimum answer lies between:
  - `0` (minimum pages)
  - `sum(arr)` (maximum pages)
- Use **binary search** to minimize the maximum pages:
  - Check if it is possible to allocate books with `mid` as max pages
  - If valid → try smaller value
  - If not valid → try larger value

---

## 💻 Code 

```java
import java.util.ArrayList;

public class Solution {
    public static int findPages(ArrayList<Integer> arr, int n, int m) {

        if (m > n) return -1;

        int sum = 0;
        for (int i = 0; i < n; i++) {
            sum += arr.get(i);
        }

        int ans = -1;
        int st = 0, e = sum;

        while (st <= e) {
            int mid = st + (e - st) / 2;

            if (isValid(arr, n, m, mid)) {
                ans = mid;
                e = mid - 1;
            } else {
                st = mid + 1;
            }
        }
        return ans;
    }

    public static boolean isValid(ArrayList<Integer> arr, int n, int m, int maxAllowedPages) {

        int students = 1;
        int pages = 0;

        for (int i = 0; i < n; i++) {

            if (arr.get(i) > maxAllowedPages)
                return false;

            if (pages + arr.get(i) <= maxAllowedPages) {
                pages += arr.get(i);
            } else {
                students++;
                pages = arr.get(i);
            }
        }
        return students <= m;
    }
}
