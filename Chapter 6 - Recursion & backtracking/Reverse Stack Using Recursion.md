# 🔁 Reverse a Stack Using Recursion

This program reverses a stack **without using any extra data structure**, relying purely on **recursion**.

---

## 📌 Problem Statement

Given a stack of integers, reverse it such that the **bottom element becomes the top**, using recursion only.

---

## 🧠 Approach

The solution uses **two recursive functions**:

### 1️⃣ `reverseStack(stack)`
- Pops the top element
- Recursively reverses the remaining stack
- Inserts the popped element at the bottom

### 2️⃣ `insertAtBottom(stack, element)`
- Inserts an element at the **bottom** of the stack recursively

---

## 💻 Code 

```java
import java.util.Stack;

public class Solution {

    public static void insertAtBottom(Stack<Integer> stack, int element) {
        if (stack.isEmpty()) {
            stack.push(element);
            return;
        }

        int top = stack.pop();
        insertAtBottom(stack, element);
        stack.push(top);
    }

    public static void reverseStack(Stack<Integer> stack) {
        if (stack.isEmpty()) {
            return;
        }

        int top = stack.pop();
        reverseStack(stack);
        insertAtBottom(stack, top);
    }
}
