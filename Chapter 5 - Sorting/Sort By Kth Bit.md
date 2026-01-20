# 🔢 Sort Array by K-th Bit 

This program sorts an array based on the **K-th bit** of each element.

- All numbers with **K-th bit = 0** come first  
- Followed by numbers with **K-th bit = 1**  
- **Relative order is preserved** (stable partition)

---

## 📌 Problem Statement

Given:
- An integer array `arr` of size `n`
- An integer `k`

Sort the array such that:
- Elements having the **k-th bit unset (0)** appear before
- Elements having the **k-th bit set (1)** appear after

---

## 🧠 Approach (Bit Manipulation)

- Convert `k` to **0-based indexing** → `k = k - 1`
- Use **bitwise AND** with `(1 << k)` to check the k-th bit
- Traverse array twice:
  1. First pass → collect elements with bit = `0`
  2. Second pass → collect elements with bit = `1`

✔ This guarantees **stable sorting**

---

## 🔄 Algorithm Steps

1. Create a result array `ans`
2. Reduce `k` by 1 (0-based bit position)
3. Traverse array and store numbers with k-th bit = `0`
4. Traverse again and store numbers with k-th bit = `1`
5. Return the result array

---

## 💻 Code 

```java
public class Solution {
    public static int[] sortArrayByKBit(int n, int k, int arr[]) {

        int[] ans = new int[n];
        int p = 0;

        k = k - 1; // convert to 0-based index

        // First pass: k-th bit = 0
        for (int i = 0; i < n; i++) {
            if ((arr[i] & (1 << k)) == 0) {
                ans[p++] = arr[i];
            }
        }

        // Second pass: k-th bit = 1
        for (int i = 0; i < n; i++) {
            if ((arr[i] & (1 << k)) != 0) {
                ans[p++] = arr[i];
            }
        }

        return ans;
    }
}
