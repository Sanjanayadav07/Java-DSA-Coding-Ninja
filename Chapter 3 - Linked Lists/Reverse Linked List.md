# 🔁 Reverse Linked List (Recursive)

## 📌 Problem Statement
You are given the **head of a singly linked list**.

Your task is to **reverse the linked list** and return the new head.

---

## 🧠 Approach (Recursion)
- If the list is empty or has only one node, return `head`
- Recursively reverse the remaining list starting from `head.next`
- Fix the current node’s links:
  - Make `head.next.next = head`
  - Set `head.next = null`
- Return the new head of the reversed list

---

## ⏱ Complexity Analysis
- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(n)` (recursive call stack)

---

## 💻 Code

```java
public class Solution {
    public static Node reverseLinkedList(Node head) {
        if (head == null || head.next == null) {
            return head;
        }

        Node newHead = reverseLinkedList(head.next);
        head.next.next = head;
        head.next = null;

        return newHead;
    }
}
