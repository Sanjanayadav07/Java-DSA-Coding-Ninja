# 🔁 Generate All Subsequences of a String 

This program generates **all non-empty subsequences** of a given string using **recursion**.

---

## 📌 Problem Statement

Given a string `str`, return an `ArrayList<String>` containing **all possible non-empty subsequences** of the string.

📌 A subsequence is formed by deleting **zero or more characters** without changing the order of remaining characters.

---

## 🧠 Approach (Recursion)

At each index, we have **two choices**:
1. ✅ Include the current character
2. ❌ Exclude the current character  

We explore both paths recursively.

---

## 🔄 Algorithm Steps

1. Start recursion from index `0`
2. Maintain a temporary list to store current subsequence
3. When end of string is reached:
   - If subsequence is non-empty → store it
4. Backtrack after each recursive call

---

## 💻 Code 

```java
import java.util.* ;
import java.io.*; 
import java.util.ArrayList;

class Solution {

    private static void getSubsequences(int idx, String str,
                                        ArrayList<Character> subsequences,
                                        ArrayList<String> allSubsequences) {

        if (idx >= str.length()) {
            if (subsequences.size() > 0) {
                String result = "";
                for (char ch : subsequences) {
                    result += ch;
                }
                allSubsequences.add(result);
            }
            return;
        }

        // Include current character
        subsequences.add(str.charAt(idx));
        getSubsequences(idx + 1, str, subsequences, allSubsequences);

        // Exclude current character (backtrack)
        subsequences.remove(subsequences.size() - 1);
        getSubsequences(idx + 1, str, subsequences, allSubsequences);
    }

    public static ArrayList<String> subsequences(String str) {
        ArrayList<Character> subsequences = new ArrayList<>();
        ArrayList<String> allSubsequences = new ArrayList<>();

        getSubsequences(0, str, subsequences, allSubsequences);
        return allSubsequences;
    }
}
