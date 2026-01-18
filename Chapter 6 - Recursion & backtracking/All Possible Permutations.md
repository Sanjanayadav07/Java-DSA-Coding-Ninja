# 🔁 String Permutations using Backtracking 

This program generates **all permutations of a given string** using the **backtracking technique**.

---

## 📌 Problem Statement

Given a string `s`, return **all possible permutations** of its characters.

---

## 🧠 Approach (Backtracking)

We build permutations **character by character**:

### 🔹 Key Ideas:
- Use a `boolean[] used` array to track which characters are already used
- Use `StringBuilder` for efficient string modification
- Backtrack after exploring each choice

---

## 🔄 Algorithm Steps

1. Start with an empty string (`temp`)
2. Try placing each unused character
3. Mark character as used
4. Recurse to build the next level
5. Backtrack (remove character & unmark)

---

## 💻 Code

```java
import java.util.*;
import java.io.*;

public class Solution {

    public static List<String> findPermutations(String s) {
        List<String> result = new ArrayList<>();
        boolean[] used = new boolean[s.length()];

        backtrack(s, new StringBuilder(), used, result);
        return result;
    }

    private static void backtrack(String s, StringBuilder temp,
                                  boolean[] used, List<String> result) {

        if (temp.length() == s.length()) {
            result.add(temp.toString());
            return;
        }

        for (int i = 0; i < s.length(); i++) {
            if (!used[i]) {
                used[i] = true;
                temp.append(s.charAt(i));

                backtrack(s, temp, used, result);

                used[i] = false;
                temp.deleteCharAt(temp.length() - 1);
            }
        }
    }
}
