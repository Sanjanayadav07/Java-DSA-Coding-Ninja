# ☎️ Phone Keypad Letter Combinations

## 📌 Problem Statement
Given a string `s` containing digits from **2 to 9**, return **all possible letter combinations** that the number could represent.

The mapping follows the traditional **mobile keypad**.

---

## 🔢 Keypad Mapping

| Digit | Letters |
|------|---------|
| 2 | abc |
| 3 | def |
| 4 | ghi |
| 5 | jkl |
| 6 | mno |
| 7 | pqrs |
| 8 | tuv |
| 9 | wxyz |

---

## 🧠 Approach (Backtracking)
- Start from index `0`
- For the current digit:
  - Try **each mapped character**
  - Add it to a temporary string
  - Recur for the next digit
- When all digits are processed → store the combination
- Backtrack by removing the last character

---

## 🔁 Recursion Flow
## digits = "23"
```
      ""
  /    |    \
 a     b     c

/ | \ / | \ / |
ad ae af ...
```

---

## ⏱ Complexity Analysis
- **Time Complexity:** `O(4^n)` (max 4 letters per digit)
- **Space Complexity:** `O(n)` (recursion stack)

---

## 💻 Code

```java
import java.util.*;

public class Solution {

    // Non-static to preserve result across recursion
    ArrayList<String> result = new ArrayList<>();

    public void solve(int idx, String s, StringBuilder temp,
                      Map<Character, String> mp) {

        if (idx >= s.length()) {
            result.add(temp.toString());
            return;
        }

        char ch = s.charAt(idx);
        String letters = mp.get(ch);

        for (int i = 0; i < letters.length(); i++) {
            temp.append(letters.charAt(i));
            solve(idx + 1, s, temp, mp);
            temp.deleteCharAt(temp.length() - 1); // backtrack
        }
    }

    public static ArrayList<String> combinations(String s) {

        Solution ob = new Solution();

        if (s.length() == 0)
            return ob.result;

        Map<Character, String> mp = new HashMap<>();
        mp.put('2', "abc");
        mp.put('3', "def");
        mp.put('4', "ghi");
        mp.put('5', "jkl");
        mp.put('6', "mno");
        mp.put('7', "pqrs");
        mp.put('8', "tuv");
        mp.put('9', "wxyz");

        ob.solve(0, s, new StringBuilder(), mp);

        return ob.result;
    }
}

