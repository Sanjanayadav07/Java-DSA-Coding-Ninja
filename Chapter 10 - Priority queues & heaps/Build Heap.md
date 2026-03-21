# 🔺 Build Max Heap

## 📌 Problem
Given an array, convert it into a **Max Heap**.

- 👉 Max Heap Property:
- Parent ≥ Children


---

## 🧠 Key Idea

To build a heap efficiently:

- Start from the **last non-leaf node**
- Apply **heapify** operation
- Move upwards till root

---

## 🛠️ Approach

### Step 1: Find Last Non-Leaf Node
- index = n/2 - 1
- Why?
- Nodes after this index are already leaf nodes → already heap

---

### Step 2: Apply Heapify Bottom-Up

- Loop from: i = n/2 - 1 → 0
- At each index:
- Fix subtree using **heapify**

---

## 🔁 Heapify Logic

For a node at index `i`:

- Left child → `2*i + 1`
- Right child → `2*i + 2`

Steps:
1️⃣ Find largest among parent, left, right  
2️⃣ Swap if needed  
3️⃣ Recursively heapify affected subtree  

---

## 💻 Code

```java
import java.util.*;

public class Solution {

    // Heapify function
    public static void heapify(ArrayList<Integer> arr, int index, int n) {

        int largest = index;
        int left = 2 * index + 1;
        int right = 2 * index + 2;

        // Check left child
        if (left < n && arr.get(left) > arr.get(largest)) {
            largest = left;
        }

        // Check right child
        if (right < n && arr.get(right) > arr.get(largest)) {
            largest = right;
        }

        // If largest is not root
        if (largest != index) {

            // Swap
            int temp = arr.get(index);
            arr.set(index, arr.get(largest));
            arr.set(largest, temp);

            // Recursively heapify
            heapify(arr, largest, n);
        }
    }

    public static ArrayList<Integer> buildHeap(ArrayList<Integer> arr, int n) {

        // Start from last non-leaf node
        for (int i = n/2 - 1; i >= 0; i--) {
            heapify(arr, i, n);
        }

        return arr;
    }
}
```
---
### ⏱️ Time Complexity
- O(N)

### 📦 Space Complexity
- O(H)
