# Compute nCr

## 📌 Problem
Find the value of:

nCr = n! / (r! * (n-r)!)

Where:
- n = total items
- r = selected items

---

## 🧠 Approach
Use factorial formula directly:

nCr = n! / (r! × (n-r)!)

---
## 🔢 code
```
import java.util.* ;
import java.io.*; 
public class Solution {
	public static int choose(int n, int r) {
		// Write your code here.
		if(n == r || r == 0) return 1;
		return (int)(fact(n)/(fact(r)* fact(n-r)));
	}
	private static long fact(int num) {
		if(num == 0 || num == 1) return 1;
		return num * fact(num-1);
	}
}
```
---

## ⚡ Complexity
- Time: O(N)
- Space: O(N) (recursive calls)
