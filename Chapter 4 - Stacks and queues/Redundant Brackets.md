# 🧩 Find Redundant Brackets 

## 📌 Problem Statement
You are given a mathematical expression in the form of a string `s`.

Your task is to **check whether the expression contains any redundant brackets**.

- Return `true` if redundant brackets are present  
- Return `false` otherwise  

> Redundant brackets are brackets that do not affect the expression,  
> e.g. `((a+b))`, `(a)`.

---

## 🧠 Approach (Using Stack)
- Use a stack to store characters
- Push opening brackets `(` and operators `+ - * /`
- When a closing bracket `)` is encountered:
  - Pop elements until `(` is found
  - Check if any operator exists inside the brackets
  - If no operator is found → brackets are redundant
- Return `true` immediately if redundant brackets are detected

---

## ⏱ Complexity Analysis
- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(n)`

---

## 💻 Code

```java
import java.util.*;
import java.io.*;

public class Solution {

    public static boolean findRedundantBrackets(String s) {

        Stack<Character> stack = new Stack<>();

        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);

            if (c == '(' || c == '+' || c == '-' || c == '*' || c == '/') {
                stack.push(c);
            } 
            else if (c == ')') {
                boolean isRedundant = true;

                while (stack.peek() != '(') {
                    char top = stack.pop();
                    if (top == '+' || top == '-' || top == '*' || top == '/') {
                        isRedundant = false;
                    }
                }
                stack.pop(); // remove '('

                if (isRedundant) {
                    return true;
                }
            }
        }
        return false;
    }
}
