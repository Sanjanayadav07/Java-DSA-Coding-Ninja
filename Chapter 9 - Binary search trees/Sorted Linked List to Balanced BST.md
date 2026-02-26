# 🌳 Convert Sorted Linked List to Balanced BST 

This program converts a **Sorted Singly Linked List** into a  
**Height Balanced Binary Search Tree (BST)**.

---

## 📌 Problem Statement

Given:
- A sorted linked list

Convert it into:
- A height-balanced BST

Such that:
✔ Inorder traversal remains sorted  
✔ Tree height is minimum  

---

## 🧠 Key Idea

👉 Middle element of list = Root of BST

Because:
- Left half → Left subtree
- Right half → Right subtree

Same logic as:
**Sorted Array → Balanced BST**


We use:
🎯 Slow & Fast Pointer to find middle node

---

## 🚀 Approach

### Step 1: Find Middle Node
Using:

``` id="mid"
slow → moves 1 step  
fast → moves 2 steps
Middle node becomes root
```
### Step 2: Break List
```
Left part → head to mid-1
Right part → mid+1 to end

```
### Step 3: Recursively Build
```
root.left  = BST from left list
root.right = BST from right list

```
---
## ⏱️ Complexity Analysis
- Total Time	O(n log n)
- Space (recursion)	O(log n)
---

## 🧑‍💻 Code
```
public class Solution {

    public static TreeNode<Integer> sortedListToBST(Node<Integer> head) {

        if (head == null) return null;

        // Single node
        if (head.next == null) {
            return new TreeNode<>(head.data);
        }

        Node<Integer> slow = head;
        Node<Integer> fast = head;
        Node<Integer> slowPrev = null;

        // Find middle
        while (fast != null && fast.next != null) {
            slowPrev = slow;
            slow = slow.next;
            fast = fast.next.next;
        }

        // Middle becomes root
        TreeNode<Integer> root = new TreeNode<>(slow.data);

        // Break left half
        slowPrev.next = null;

        // Recursively build BST
        root.left = sortedListToBST(head);
        root.right = sortedListToBST(slow.next);

        return root;
    }
}
```
