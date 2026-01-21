# 🔢 Sort by Set Bits Count 

This program sorts an array based on the **number of set bits (1s)** in the binary representation of each element.

- Elements with **more set bits come first**
- Sorting is done using a **custom comparator**

---

## 📌 Problem Statement

Given an `ArrayList<Integer>` of size `n`, sort the list in **descending order of set bits count** for each number.

---

## 🧠 Approach

Java provides a built-in method:
- `Integer.bitCount(x)` → returns number of set bits in `x`

We use:
- `Collections.sort()` with a **lambda comparator**
- Compare elements based on their set bit counts

---

## 🔄 Algorithm Steps

1. Use `Collections.sort()` on the array list
2. Compare two elements using `Integer.bitCount()`
3. Sort in descending order of set bits

---

## 💻 Code

```java
import java.util.* ;
import java.io.*; 

public class Solution {
    public static void sortSetBitsCount(ArrayList<Integer> arr, int size) {
        Collections.sort(arr, (o1, o2) ->
            (Integer.bitCount(o2) - Integer.bitCount(o1))
        );
    }
}
