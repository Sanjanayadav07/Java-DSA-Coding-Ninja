# 🔗 Generate Balanced Parentheses 

This program prints **all valid combinations of balanced parentheses** using **recursion and backtracking**.

---

## 📌 Problem Statement

Given an integer `n`, generate all combinations of **balanced parentheses** using `{` and `}` such that:
- Every opening brace has a matching closing brace
- At no point do closing braces exceed opening braces

---

## 🧠 Approach (Recursion + Backtracking)

We keep track of:
- `oc` → number of **open braces remaining**
- `cc` → number of **close braces remaining**

### 🔹 Rules:
1. You can add `{` **if `oc > 0`**
2. You can add `}` **only if `cc > oc`**
3. A valid sequence is formed when `oc == 0 && cc == 0`

---

## 🔄 Algorithm Steps

1. Start with empty string `""`
2. Add `{` if open count remains
3. Add `}` only when it won’t break balance
4. Print when both counts reach zero

---

## 💻 Code 

```java
public class Solution {

    public static void solve(String temp, int oc, int cc) {
        // oc -> open count, cc -> close count
        if (oc == 0 && cc == 0) {
            System.out.println(temp);
            return;
        }

        if (oc != 0) {
            solve(temp + "{", oc - 1, cc);
        }

        if (oc < cc) {
            solve(temp + "}", oc, cc - 1);
        }
    }

    public static void printParentheses(int n) {
        solve("", n, n);
    }
}
