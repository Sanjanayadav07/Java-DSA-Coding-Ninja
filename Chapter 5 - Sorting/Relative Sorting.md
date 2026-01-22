# 🔢 Relative Sorting of an Array

This program sorts one array **relative to the order of another array**, and places remaining elements in **ascending order**.

---

## 📌 Problem Statement

Given:
- `arr` → main list of integers (size `n`)
- `brr` → reference list defining relative order (size `m`)

Tasks:
1. Sort elements of `arr` according to the order in `brr`
2. Elements **not present in `brr`** should appear at the end in **sorted order**

---

## 🧠 Approach

- Use a **TreeMap** to store frequency of elements in `arr`
- Traverse `brr`:
  - Add matching elements to result based on frequency
  - Set their frequency to 0
- Traverse remaining elements in TreeMap:
  - Add leftover elements in sorted order

`TreeMap` ensures automatic sorting of remaining elements.

---

## 💻 Code 

```java
import java.util.*;

public class Solution {

    public static List<Integer> relativeSorting(List<Integer> arr, List<Integer> brr, int n, int m) {

        TreeMap<Integer, Integer> hashMap = new TreeMap<>();

        // Count frequency of elements in arr
        for (Integer integer : arr) {
            hashMap.put(integer, hashMap.getOrDefault(integer, 0) + 1);
        }

        List<Integer> result = new ArrayList<>();

        // Add elements according to brr order
        for (Integer integer : brr) {
            int value = hashMap.getOrDefault(integer, 0);
            while (value > 0) {
                result.add(integer);
                value--;
            }
            hashMap.put(integer, 0);
        }

        // Add remaining elements in sorted order
        for (Map.Entry<Integer, Integer> entry : hashMap.entrySet()) {
            int value = entry.getValue();
            while (value > 0) {
                result.add(entry.getKey());
                value--;
            }
        }

        return result;
    }
}
