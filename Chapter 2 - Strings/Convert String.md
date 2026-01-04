# 🔤 Convert String 

## 📌 Problem Statement
You are given a string `str`.

Your task is to **capitalize the first letter of each word** in the string and return the modified string.

---

## 🧠 Approach
- Convert the string into a character array
- Capitalize the first character
- Traverse the array:
  - If a space `' '` is found, capitalize the next character
- Convert the character array back to a string

---

## ⏱ Complexity Analysis
- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(n)` (for character array)

---

## 💻 Code

```java
import java.util.*;
import java.io.*;

public class Solution {
    public static String convertString(String str) {
        char[] ch = str.toCharArray();

        ch[0] = Character.toUpperCase(ch[0]);

        for (int i = 0; i < ch.length - 1; i++) {
            if (ch[i] == ' ') {
                ch[i + 1] = Character.toUpperCase(ch[i + 1]);
            }
        }
        return new String(ch);
    }
}
