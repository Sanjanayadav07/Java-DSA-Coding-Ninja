# 🌐 Generate Valid IP Addresses 

This program generates **all valid IP addresses** from a given numeric string using **recursion and backtracking**.

---

## 📌 Problem Statement

Given a string containing only digits, return all possible **valid IP addresses** that can be formed by inserting dots (`.`).

### 🔹 IP Address Rules
- Exactly **4 parts**
- Each part is between **0 and 255**
- No leading zeros (except `"0"` itself)

---

## 🧠 Approach (Backtracking)

We split the string into **4 valid segments**, where each segment:
- Has length **1 to 3**
- Is numerically valid (`0–255`)
- Does not start with `'0'` unless it is `"0"`

---

## 🔄 Algorithm Steps

1. Start from index `0` and part `0`
2. Try segments of length **1, 2, and 3**
3. Validate each segment
4. Recurse for the next segment
5. If 4 parts are formed and string is fully used → store result

---

## 💻 Code 

```java
import java.util.*;
import java.io.*;

public class Solution {
    
    public static List<String> generateIPAddress(String s) {
        List<String> result = new ArrayList<>();
        int n = s.length();
        
        // If length > 12, IP cannot be formed
        if (n > 12) return result;
        
        solve(s, 0, 0, "", result, n);
        return result;
    }
    
    private static void solve(String s, int idx, int part, String curr,
                              List<String> result, int n) {
        
        // Valid IP formed
        if (idx == n && part == 4) {
            result.add(curr.substring(0, curr.length() - 1)); // remove extra dot
            return;
        }
        
        // Invalid case
        if (part >= 4 || idx >= n) return;

        // 1-digit segment
        solve(s, idx + 1, part + 1, curr + s.substring(idx, idx + 1) + ".", result, n);

        // 2-digit segment
        if (idx + 2 <= n) {
            String seg = s.substring(idx, idx + 2);
            if (isValid(seg))
                solve(s, idx + 2, part + 1, curr + seg + ".", result, n);
        }

        // 3-digit segment
        if (idx + 3 <= n) {
            String seg = s.substring(idx, idx + 3);
            if (isValid(seg))
                solve(s, idx + 3, part + 1, curr + seg + ".", result, n);
        }
    }
    
    // Check if segment is valid
    private static boolean isValid(String str) {
        if (str.length() > 1 && str.charAt(0) == '0') return false;
        int val = Integer.parseInt(str);
        return val <= 255;
    }
}
