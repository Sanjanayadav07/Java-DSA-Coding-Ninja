# 🌊 Wave Form Array 

This program converts a given array into a **wave form**, where elements follow the pattern:
```
arr[0] ≥ arr[1] ≤ arr[2] ≥ arr[3] ≤ ...

```

---

## 📌 Problem Statement

Given an integer array `arr` of size `n`, rearrange the elements to form a **wave array**.

---

## 🧠 Approach

### Step 1: Sort the Array
Sorting ensures that smaller and larger elements are placed correctly.

### Step 2: Swap Adjacent Elements
Swap every alternate pair:
- Swap `arr[0]` with `arr[1]`
- Swap `arr[2]` with `arr[3]`
- Continue till the end

This guarantees the wave pattern.

---

## 🔄 Algorithm Steps

1. Sort the array
2. Traverse the array with step size `2`
3. Swap `arr[i]` and `arr[i+1]`
4. Return the modified array

---

## 💻 Code 

```java
import java.util.*;

public class Solution {

    public static int[] waveFormArray(int[] arr, int n) {

        // STEP 1: Sort the array
        Arrays.sort(arr);

        // STEP 2: Create wave form
        for (int i = 0; i < n - 1; i += 2) {
            int temp = arr[i];
            arr[i] = arr[i + 1];
            arr[i + 1] = temp;
        }

        return arr;
    }
}

