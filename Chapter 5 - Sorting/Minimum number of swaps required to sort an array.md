# 🔁 Minimum Swaps to Sort an Array 

This program calculates the **minimum number of swaps** required to sort an array in **ascending order** using a **selection sort–based approach**.

---

## 📌 Problem Statement

Given an integer array, determine the minimum number of swaps required to sort the array.

---

## 🧠 Approach (Selection Sort Logic)

- Traverse the array from left to right
- For each index `i`:
  - Find the minimum element in the remaining unsorted part
  - If it’s not already at index `i`, swap it
  - Count each swap

This guarantees that each element is placed at its correct position with **minimum swaps per position**.

---

## 💻 Code 
```java
public class Solution {
	public static int minSwaps(int[] arr) {
		int n = arr.length;
		int swaps = 0;

		for (int i = 0; i < n; i++) {
			int minIndex = i;

			for (int j = i + 1; j < n; j++) {
				if (arr[j] < arr[minIndex]) {
					minIndex = j;
				}
			}

			if (minIndex != i) {
				int temp = arr[i];
				arr[i] = arr[minIndex];
				arr[minIndex] = temp;
				swaps++;
			}
		}
		return swaps;
	}
}
