# 🔄 Convert Min Heap to Max Heap

## 📌 Problem
Given a **Min Heap (array representation)**, convert it into a **Max Heap**.

👉 Min Heap:

Parent ≤ Children


👉 Max Heap:

Parent ≥ Children


---

## 🧠 Key Idea

- We can convert a Min Heap to a Max Heap by:

- ✔ Applying **Max Heapify** from bottom to top  
- ✔ Starting from the **last non-leaf node**

---

## 🛠️ Approach

### Step 1: Start from Last Non-Leaf Node
- i = n/2 - 1

---

### Step 2: Apply Heapify

- Loop: i → 0
- At each index:
- Fix subtree using **max heapify**

---

## 🔁 Heapify Logic

For index `i`:

- Left child → `2*i + 1`  
- Right child → `2*i + 2`  

Steps:
- 1️⃣ Find largest among parent, left, right  
- 2️⃣ Swap if needed  
- 3️⃣ Recursively heapify  

---

## 💻 Code

```java
import java.util.*;

public class Solution {

    // Max Heapify
    public static void heapify(long[] arr, int index, int n) {

        int largest = index;
        int left = 2 * index + 1;
        int right = 2 * index + 2;

        // Left child
        if (left < n && arr[left] > arr[largest]) {
            largest = left;
        }

        // Right child
        if (right < n && arr[right] > arr[largest]) {
            largest = right;
        }

        // Swap if needed
        if (largest != index) {

            long temp = arr[index];
            arr[index] = arr[largest];
            arr[largest] = temp;

            heapify(arr, largest, n);
        }
    }

    public static void minHeapToMaxHeap(long[] arr) {

        int n = arr.length;

        // Build Max Heap
        for (int i = n/2 - 1; i >= 0; i--) {
            heapify(arr, i, n);
        }
    }
}
```
---
### ⏱️ Time Complexity
- O(N)

- ✔ Bottom-up heap construction
- ✔ More efficient than inserting elements one by one

### 📦 Space Complexity
- O(H)
- Recursive stack space
H ≈ log N
