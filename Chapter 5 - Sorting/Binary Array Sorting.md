# 🔢 Sort Binary Array (0s and 1s) 

This program sorts a binary array consisting only of **0s and 1s** using an efficient **two-pointer approach**.

---

## 📌 Problem Statement

Given an `ArrayList<Integer>` containing only `0` and `1`, sort the array such that:
- All `0`s come before all `1`s
- Do this efficiently without using extra space

---

## 🧠 Approach (Two Pointers)

- Use two pointers:
  - `l` → start of the array
  - `r` → end of the array
- Rules:
  - If `arr[l] == 0` → move `l` forward
  - If `arr[r] == 1` → move `r` backward
  - Else → swap `arr[l]` and `arr[r]`, then move both pointers

This ensures all `0`s move left and all `1`s move right.

---

## 💻 Code 

```java
import java.util.ArrayList;

public class Solution {
	public static ArrayList<Integer> sortBinaryArray(ArrayList<Integer> arr, int n) {
		int l = 0, r = n - 1;

		while (l < r) {
			if (arr.get(l) == 0) {
				l++;
			} else if (arr.get(r) == 1) {
				r--;
			} else {
				int temp = arr.get(l);
				arr.set(l, arr.get(r));
				arr.set(r, temp);
				l++;
				r--;
			}
		}
		return arr;
	}
}
