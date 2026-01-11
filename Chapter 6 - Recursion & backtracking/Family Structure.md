# 👶 Kth Child in Nth Generation 

## 📌 Problem Statement
You are given two integers:
- `n` → generation number  
- `k` → position of the child in that generation  

In the **first generation**, there is only **one Male child**.

Rules:
- Every **Male** produces **Male → Female**
- Every **Female** produces **Female → Male**

Your task is to determine the **gender of the k-th child in the n-th generation**.

Return:
- `"Male"` or `"Female"`

---

## 🧠 Approach
- Start from the given `n` and `k`
- Traverse **upwards from generation n to generation 1**
- If `k` is even:
  - Move to parent `k / 2`
  - Flip gender
- If `k` is odd:
  - Move to parent `(k + 1) / 2`
- Continue until generation becomes 1
- If gender flips are even → **Male**
- If odd → **Female**

---

## ⏱ Complexity Analysis
- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(1)`

---

## 💻 Code

```java
public class Solution {

    public static String kthChildNthGeneration(int n, long k) {

        boolean gender = false; // false -> Male, true -> Female

        while (n > 1) {
            if (k % 2 == 0) {
                k = k / 2;
                gender = !gender;
            } else {
                k = (k + 1) / 2;
            }
            n--;
        }

        return gender ? "Female" : "Male";
    }
}
