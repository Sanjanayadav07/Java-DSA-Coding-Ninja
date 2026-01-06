# 🔍 Search in Linked List 

## 📌 Problem Statement
You are given the **head of a singly linked list** and an integer `k`.

Your task is to check whether the value `k` is present in the linked list.

- Return `1` if `k` is found  
- Return `0` if `k` is not found  

---

## 🧠 Approach
- Start from the head node
- Traverse the linked list using a temporary pointer
- Compare each node’s data with `k`
- Return `1` as soon as a match is found
- If the traversal ends, return `0`

---

## ⏱ Complexity Analysis
- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(1)`

---

## 💻 Code

```java
public class Solution {
    public static int searchInLinkedList(Node head, int k) {
        Node temp = head;

        while (temp != null) {
            if (temp.data == k) {
                return 1;
            }
            temp = temp.next;
        }
        return 0;
    }
}
