# 🌳 Total BSTs for Each Element as Root 

This program calculates the **number of unique BSTs possible when each element of the array is chosen as root**.

All calculations are performed under:
**MOD = 10^9 + 7**

---

## 📌 Problem Understanding

Given:
- An integer array `arr[]`
- Size `n`

For every element `arr[k]`, we:

1. Count how many elements are **less than it**
2. Count how many elements are **greater than it**
3. Compute:
**Total BSTs = Catalan(lessThan) × Catalan(greaterThan)**

Why?

Because:
- All smaller elements must go to left subtree
- All greater elements must go to right subtree
- Left and right subtree structures are independent

---

## 🧠 Core Concept

Number of BSTs with `n` distinct keys:
**Catalan(n) = (2n)! / ((n+1)! * n!)**

Since division under modulo isn’t direct,
we use:

- 🔹 Factorials
- 🔹 Modular Inverse
- 🔹 Extended Euclidean Algorithm

---

## 🚀 Approach

### Step 1: Precompute Factorials
Up to `2n` for Catalan formula.

### Step 2: Sort Copy of Array
To determine how many elements are:
- Less than current
- Greater than current

### Step 3: For Each Element
```
lessThan = index in sorted array
greaterThan = n - index - 1

answer = Catalan(lessThan) × Catalan(greaterThan)
```

---

## 🧑‍💻 Code

```java
import java.util.Arrays;
class XY {
    int x, y;
    XY(int a, int b) {
        x = a;
        y = b;
    }
}
public class Solution {
    public static int mod = 1000000007;
    // Multiplication of big numbers under mod.
    public static int multiply(int a, int b, int mod) {
        return (int) ((a * 1l * b) % mod);
    }
    // Precompute the factorial.
    public static void calculateFactorials(int[] factorial, int n) {
        factorial[1] = 1;
        factorial[0] = 1;
        for (int i = 2; i <= 2 * n; i++) {
            factorial[i] = multiply(factorial[i - 1], i, mod);
        }
    }
    public static int gcdExtended(int a, int b, XY xy) {
        // Base Case.
        if (a == 0) {
            xy.x = 0;
            xy.y = 1;
            return b;

        }
        // To store results of recursive call.

        XY xy1 = new XY(1, 1); 
        int gcd = gcdExtended(b % a, a, xy1);
        // Update x and y using results of recursive call.
        xy.x = xy1.y - (b / a) * xy1.x;

        xy.y = xy1.x;

 

        return gcd;

    }

 

    public static int modInverse(int b, int m) {

 

        // Used in extended GCD algorithm.

        XY xy = new XY(1, 1); 

        int g = gcdExtended(b, m, xy);

 

        // Return -1 if b and m are not co-prime.

        if (g != 1) {

            return -1;

        }

 

        // m is added to handle negative x.

        return (xy.x % m + m) % m;

    }

 

    // Returns catalan(n) % 1e9+7.

    public static int catalan(int n, int[] factorial) {

        int mI1 = modInverse(factorial[n + 1], mod);

        int mI2 = modInverse(factorial[n], mod);
        int mul1 = multiply(factorial[2 * n], mI1, mod);
        return multiply(mul1, mI2, mod);

    }

    public static int[] totalBST(int[] arr, int n) {

        int[] ansArray = new int[n];
        int[] factorial = new int[2 * n + 1];

        calculateFactorials(factorial, n);
        int[] sortedCopy = arr.clone();
        // Sort for efficient searching.

        Arrays.sort(sortedCopy);
        // For each array element.

        for (int k = 0; k < n; k++) {

            /*

                Find the position of the current element in sorted order.

                arr[k] will be present in the array.

            */

            int pos = Arrays.binarySearch(sortedCopy, arr[k]); 
            /*

                To find the lower bound of element.

                If the number is not present.

            */  

            if (pos < 0) {

                pos = Math.abs(pos) - 1;

            } 
            // If the number is present we are checking.

            else { 
                // Whether the number is present multiple times or not.

                int y = sortedCopy[pos];

                for (int i = pos - 1; i >= 0; i--) {

                    if (sortedCopy[i] == y) {

                        -- pos;

                    } 

                    else {

                        break;

                    }

                }

            }
            // No of elements less = pos.
            int lessThan = pos;
            // No of elements greater = n - pos - 1.
            int greaterThan = n - pos - 1;
            // Find catalan number to the left and right.

            int ansLeft = catalan(lessThan, factorial);
            int ansRight = catalan(greaterThan, factorial);
            int ans = multiply(ansLeft, ansRight, mod);
            ansArray[k] = ans;
        }
        return ansArray;

    }

}
