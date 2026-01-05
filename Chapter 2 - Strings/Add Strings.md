# 🔢 String Concatenation (Addition Using BigInteger)

## 📌 Problem Statement
You are given two numbers `num1` and `num2` in **string format**.

Your task is to **add both numbers** and return the result as a string.

> Note: The numbers can be very large, so you cannot convert them directly using primitive data types.

---

## 🧠 Approach
- Convert both string numbers into `BigInteger`
- Add the two `BigInteger` values
- Convert the result back to a string
- Return the final string

---

## ⏱ Complexity Analysis
- **Time Complexity:** `O(n)`  
- **Space Complexity:** `O(n)`

(where `n` is the length of the larger string)

---

## 💻 Code

```java
import java.util.*;
import java.io.*;
import java.math.BigInteger;

public class Solution {

    public static String stringConcatenation(String num1, String num2) {
        BigInteger s1 = new BigInteger(num1);
        BigInteger s2 = new BigInteger(num2);

        BigInteger sum = s1.add(s2);
        return sum.toString();
    }
}
