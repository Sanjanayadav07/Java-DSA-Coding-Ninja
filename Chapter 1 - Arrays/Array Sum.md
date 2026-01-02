
## 📌 Problem Statement
You are given an integer array `arr` of size `n`.

Your task is to return the **sum of all elements** present in the array.

---

## 🧠 Approach
- Initialize a variable `sum` with `0`
- Traverse the array using a loop
- Add each element to `sum`
- Return the final sum

---

## ⏱ Complexity Analysis
- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(1)`

---

## 💻 Code

```java
import java.util.*;

public class Solution {
    public static int arraySum(int[] arr, int n) {
        int sum = 0;

        for (int i = 0; i < arr.length; i++) {
            sum += arr[i];
        }
        return sum;
    }
}
