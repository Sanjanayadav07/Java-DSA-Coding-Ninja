# 🟡 Find Middle of Linked List 

## 📌 Problem Statement
You are given the **head of a singly linked list**.

Your task is to **find and return the middle node** of the linked list.

> If the linked list has an even number of nodes, return the **second middle node**.

---

## 🧠 Approach (Slow & Fast Pointer)
- Initialize two pointers:
  - `slow` moves one step at a time
  - `fast` moves two steps at a time
- When `fast` reaches the end, `slow` will be at the middle
- Return the node pointed to by `slow`

---

## ⏱ Complexity Analysis
- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(1)`

---

## 💻 Code

```java
public class Solution {
    public static Node findMiddle(Node head) {
        Node slow = head;
        Node fast = head;

        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }
}
