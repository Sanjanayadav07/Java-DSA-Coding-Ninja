# 🔢 Generate Binary Strings Without Consecutive 1s 

## 📌 Problem Statement
Given an integer `N`, generate **all binary strings of length N** such that:
- The string contains **no two consecutive '1's**

Return the list of all valid strings.

---

## 🧠 Approach (Recursion / Backtracking)
- Build the string character by character
- At each step:
  - Always allowed to add `'0'`
  - Add `'1'` **only if the previous character is not `'1'`**
- When the string length reaches `N`, store it

---

## 🔁 Recursive Logic
```
 If length == N → store
Else:
├── add '0'
└── add '1' (only if last char != '1')
```

---

## ⏱ Complexity Analysis
- **Time Complexity:** `O(2^N)`
- **Space Complexity:** `O(N)` (recursion stack)

---

## 💻 Code
```java
import java.util.List;
import java.util.ArrayList;

public class Solution {

    public static List<String> generateString(int N) {

        List<String> sol = new ArrayList<>();
        generateBinarySol(N, sol, "");
        return sol;
    }

    public static void generateBinarySol(int N, List<String> sol, String str) {

        if (str.length() == N) {
            sol.add(str);
            return;
        }

        // Always add '0'
        generateBinarySol(N, sol, str + "0");

        // Add '1' only if previous char is not '1'
        if (str.length() == 0 || str.charAt(str.length() - 1) != '1') {
            generateBinarySol(N, sol, str + "1");
        }
    }
}
