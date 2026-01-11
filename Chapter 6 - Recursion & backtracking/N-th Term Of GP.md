# 📐 Nth Term of Geometric Progression

## 📌 Problem Statement
You are given:
- `N` → the term number  
- `A` → the first term of the GP  
- `R` → the common ratio  

Your task is to **find the Nth term of the geometric progression** under modulo  
`10^9 + 7`.

Formula:
Nth Term = A × R^(N-1)

---

## 🧠 Approach (Fast Exponentiation)
- Direct power calculation may cause overflow
- Use **binary exponentiation (divide & conquer)** to compute `R^(N-1)` efficiently
- Multiply the result with `A` and take modulo at each step

---

## ⏱ Complexity Analysis
- **Time Complexity:** `O(log N)`
- **Space Complexity:** `O(log N)` (recursive call stack)

---

## 💻 Code

```java
public class Solution {

    public static int nthTermOfGP(int N, int A, int R) {

        int mod = 1000000007;
        long ans = (A * pow(R, N - 1, mod)) % mod;
        return (int) ans;
    }

    public static long pow(int R, int N, int mod) {

        if (N == 0) {
            return 1;
        }

        long temp = pow(R, N / 2, mod) % mod;

        if (N % 2 == 0) {
            return (temp * temp) % mod;
        } else {
            return ((temp * temp) % mod * R) % mod;
        }
    }
}
