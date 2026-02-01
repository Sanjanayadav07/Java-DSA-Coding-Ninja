# 🔍 Pair Sum in Rotated Sorted Array

## 🧩 Problem Statement
Given a **rotated sorted array** `arr[]` and an integer `target`,  
determine whether there exists **any pair of elements** in the array whose **sum equals `target`**.

---

## 💡 Approach

1. Traverse the array element by element.
2. For each element `arr[i]`, calculate its **complement**:
```
complement = target - arr[i]
```
3. Search for the complement in the **remaining part of the array** using
**Binary Search modified for a rotated sorted array**.
4. If found → return `true`
5. If no such pair exists → return `false`

This approach avoids brute force and improves efficiency.

---
## ⏱️ Time & Space Complexity

### ⏳ Time Complexity
- Outer loop runs `N` times
- For each element, **Binary Search** takes `O(log N)`

➡️ **Overall Time Complexity:**  
\[
O(N \log N)
\]

---

### 🧠 Space Complexity
- Uses constant extra space
- No additional data structures used

➡️ **Space Complexity:**  
\[
O(1)
\]

---

### 📌 Notes
- Binary Search is adapted for **rotated sorted array**
- Efficient approach compared to brute force `O(N²)`


---

## 🧠 Code

```java
import java.util.*;
import java.io.*;

public class Solution 
{
    // Function to search in rotated sorted array
    private static boolean binarySearch(int[] arr, int target, int low, int high) {
        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (arr[mid] == target) return true;

            // Left half sorted
            if (arr[low] <= arr[mid]) {
                if (arr[low] <= target && target < arr[mid]) {
                    high = mid - 1;
                } else {
                    low = mid + 1;
                }
            }
            // Right half sorted
            else {
                if (arr[mid] < target && target <= arr[high]) {
                    low = mid + 1;
                } else {
                    high = mid - 1;
                }
            }
        }
        return false;
    }

    public static boolean findPairSum(int[] arr, int target) 
    {
        int n = arr.length;
        for (int i = 0; i < n - 1; i++) {
            int complement = target - arr[i];
            if (binarySearch(arr, complement, i + 1, n - 1)) {
                return true;
            }
        }
        return false;
    }
}



