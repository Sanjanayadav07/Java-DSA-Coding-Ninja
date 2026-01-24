# 🔎 Search in a 2D Matrix 

Search a target element in a **row-wise and column-wise sorted 2D matrix** using **binary search**.

---

## 📌 Problem Statement

Given a 2D matrix represented as `ArrayList<ArrayList<Integer>>`, where:
- Each row is sorted
- The first element of each row is greater than the last element of the previous row

Determine whether a given element `x` exists in the matrix.

Return:
- `true` if found  
- `false` otherwise  

---
## ⏱️ Complexity Analysis

 - Time Complexity: O(log(m × n))
 - Space Complexity: O(1)
---
## 🧠 Approach

- Treat the 2D matrix as a **1D sorted array**
- Use binary search from `0` to `m * n - 1`
- Convert mid index to:
  - `row = mid / n`
  - `col = mid % n`
- Compare matrix value with `x`

---

## 💻 Code 

```java
import java.util.* ;
import java.io.*; 
import java.util.ArrayList;

public class Solution 
{
    public static boolean findInMatrix(int x, ArrayList<ArrayList<Integer>> arr)
    {
        int m = arr.size();
        int n = arr.get(0).size();

        int start = 0, end = m * n - 1;

        while (start <= end) {
            int mid = start + (end - start) / 2;
            int row = mid / n;
            int col = mid % n;

            if (arr.get(row).get(col) > x) {
                end = mid - 1;
            } else if (arr.get(row).get(col) < x) {
                start = mid + 1;
            } else {
                return true;
            }
        }
        return false;
    }
}
