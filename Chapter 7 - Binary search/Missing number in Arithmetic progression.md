# 🔍 Missing Number in Arithmetic Progression 

## 📌 Problem Statement
You are given an array of size **N** representing an **Arithmetic Progression (AP)** with **one missing number**.
Find the missing number efficiently.

---

## 🧠 Approach
1. Calculate common difference:
   d = (arr[n-1] - arr[0]) / n
2. Apply Binary Search.
3. Find the first index where:
   arr[mid] ≠ arr[0] + mid × d
4. Missing number = arr[0] + index × d

---

## 💻 Code

```java
import java.util.*;
import java.io.*;

public class Solution {
    public static int missingNumber(int[] arr, int n) {

        int d = (arr[n - 1] - arr[0]) / n;
        int l = 0, h = n - 1;

        while (l <= h) {
            int mid = l + (h - l) / 2;
            int expected = arr[0] + mid * d;

            if (arr[mid] == expected) {
                l = mid + 1;
            } else {
                h = mid - 1;
            }
        }
        return arr[0] + l * d;
    }
}
```
---

## ⏱️ Complexity

Time Complexity: O(log N)  
Space Complexity: O(1)

---

