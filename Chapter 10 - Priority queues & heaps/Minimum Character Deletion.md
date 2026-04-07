# 🔤 Minimum Character Deletions (Unique Frequencies)

## 📌 Problem
- Given a string `str`,  
- remove minimum characters so that **no two characters have the same frequency**.

---

## 🧠 Key Idea

- 👉 Count frequency of each character  
- 👉 Ensure all frequencies are **unique**  
- 👉 If duplicate → reduce frequency (delete chars)

---

## 🛠️ Approach

### 🔹 Step 1: Count Frequencies

- Use HashMap

---

### 🔹 Step 2: Make Frequencies Unique

- 👉 Use a **HashSet** to track used frequencies  


- while freq already exists:
- freq--
- deletion++


---

## 💻  Code

```java
import java.util.*;

public class Solution {

    public static int minCharDeletion(String str) {

        Map<Character, Integer> map = new HashMap<>();
        int ans = 0;
        Set<Integer> set = new HashSet<>();

        // Count frequencies
        for (char c : str.toCharArray()) {
            map.put(c, map.getOrDefault(c, 0) + 1);
        }

        // Make frequencies unique
        for (int freq : map.values()) {

            while (freq > 0 && set.contains(freq)) {
                freq--;
                ans++;
            }

            set.add(freq);
        }

        return ans;
    }
}
```
---
### ⏱️ Time Complexity
- O(N)
- Counting → O(N)
- Adjusting freq → O(26) ≈ constant
### 📦 Space Complexity
- O(1)
- Max 26 characters (lowercase assumption)
