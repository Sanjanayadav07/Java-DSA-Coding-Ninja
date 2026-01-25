# 🔎 Search in a 2D Matrix 

Search a target element in a **sorted 2D matrix** using the **staircase search approach**.

---

## 📌 Problem Statement

Given a 2D matrix represented as `ArrayList<ArrayList<Integer>>` where:
- Each row is sorted in ascending order
- Each column is sorted in ascending order

Determine whether a given element `x` exists in the matrix.

Return:
- `true` if found  
- `false` otherwise  

---
## ⏱️ Complexity Analysis

- Time Complexity: O(m + n)
- Space Complexity: O(1)
---
## 🧠 Approach (Staircase Search)

- Start from the **top-right corner**
- If current element equals `x` → return `true`
- If current element is greater than `x` → move **left**
- If current element is smaller than `x` → move **down**
- Continue until indices go out of bounds

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

        int r = 0, c = n - 1;

        while (r < m && c >= 0) {
            if (x == arr.get(r).get(c)) {
                return true;
            } else if (x < arr.get(r).get(c)) {
                c--;
            } else {
                r++;
            }
        }
        return false;
    }
}
