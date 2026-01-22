# 🔀 Sort a Half-Sorted Array 

This program sorts an array where **two halves are already individually sorted**, but the overall array is not fully sorted.

---

## 📌 Problem Statement

You are given an `ArrayList<Integer>` where:
- The array consists of **two sorted subarrays**
- These subarrays are placed consecutively
- You need to **merge them into a single sorted array in-place**

---

## 🧠 Approach

1. **Find the partition index**
   - Traverse the array to find the first index `i` where  
     `arr[i] > arr[i + 1]`
   - This index separates the two sorted halves

2. **Merge the two sorted parts**
   - Use two pointers:
     - One for the first half
     - One for the second half
   - Merge them like the merge step of Merge Sort

3. **Copy merged result back**
   - Replace original elements with merged elements

---

## 💻 Code 

```java
import java.util.* ;
import java.io.*; 

public class Solution {
    public static void sortHalfSorted(ArrayList<Integer> arr) {
        int n = arr.size();
        
        // Step 1: Find partition index
        int breakIdx = -1;
        for (int i = 0; i < n - 1; i++) {
            if (arr.get(i) > arr.get(i + 1)) {
                breakIdx = i;
                break;
            }
        }

        // If array is already fully sorted
        if (breakIdx == -1) return;

        // Step 2: Merge two sorted parts
        ArrayList<Integer> temp = new ArrayList<>();
        int i = 0, j = breakIdx + 1;

        while (i <= breakIdx && j < n) {
            if (arr.get(i) <= arr.get(j)) {
                temp.add(arr.get(i++));
            } else {
                temp.add(arr.get(j++));
            }
        }

        // Remaining elements
        while (i <= breakIdx) temp.add(arr.get(i++));
        while (j < n) temp.add(arr.get(j++));

        // Step 3: Copy back
        for (int k = 0; k < n; k++) {
            arr.set(k, temp.get(k));
        }
    }
}
