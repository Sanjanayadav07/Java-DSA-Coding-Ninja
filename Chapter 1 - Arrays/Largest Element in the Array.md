# 🏆 Largest Element in an Array 

## 📌 Problem Statement
You are given an integer array `arr` of size `n`.

Your task is to find and return the **largest element** present in the array.

---

## 🧠 Approach
- Initialize `maxElement` with the first element of the array
- Traverse the array from left to right
- If the current element is greater than `maxElement`, update it
- After traversal, return `maxElement`

---

## ⏱ Complexity Analysis
- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(1)`

---

## 💻 Code

```java
import java.util.*;
import java.io.*;

public class Solution {

    static int largestElement(int[] arr, int n) {
        int maxElement = arr[0];

        for (int i = 0; i < arr.length; i++) {
            if (arr[i] > maxElement) {
                maxElement = arr[i];
            }
        }
        return maxElement;
    }
}
