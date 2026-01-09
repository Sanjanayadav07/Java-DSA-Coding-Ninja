# ✅ Valid Parentheses 

## 📌 Problem Statement
You are given a string `s` consisting of parentheses `()`, `{}`, and `[]`.

Your task is to determine whether the string is **valid**.

A string is considered valid if:
- Every opening bracket has a corresponding closing bracket
- Brackets are closed in the correct order

---

## 🧠 Approach (Using Stack)
- Use a stack to store expected closing brackets
- Traverse the string character by character:
  - If an opening bracket is found, push its corresponding closing bracket
  - If a closing bracket is found:
    - Check if the stack is empty or the top does not match
    - If so, return `false`
- At the end, the stack should be empty for the string to be valid

---

## ⏱ Complexity Analysis
- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(n)`

---

## 💻 Code

```java
import java.util.*;
import java.util.Stack;

public class Solution {
    public static boolean isValidParenthesis(String s) {
        Stack<Character> stack = new Stack<>();

        for (char c : s.toCharArray()) {
            if (c == '(') {
                stack.push(')');
            } else if (c == '{') {
                stack.push('}');
            } else if (c == '[') {
                stack.push(']');
            } else {
                if (stack.isEmpty() || stack.pop() != c) {
                    return false;
                }
            }
        }
        return stack.isEmpty();
    }
}
