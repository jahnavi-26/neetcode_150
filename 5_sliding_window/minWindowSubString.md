# Problem: Minimum Window Substring

## 📄 Problem Statement
strings s and t of lengths m and n respectively, return the minimum window substring of s such that 
every character in t (including duplicates) is included in the window. If there is no such substring, 
return the empty string "".

Input: s = "ADOBECODEBANC", t = "ABC"
Output: "BANC"
Explanation: The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.

Input: s = "a", t = "aa"
Output: ""
Explanation: Both 'a's from t must be included in the window.
Since the largest window of s only has one 'a', return empty string.
---

## 🧠 Brute Force Approach
### Idea
- generate all the substrings
- store t's freq in a hashmap char, freq
- start from i, go j one by one, if new char, add in hashmap with -1
- if already positive number is present in hashmap, it's value will be zero and increase count by 1 as we see one matching char
- when count = t's len - we have got the string - could or could not be the minimum, store it's starting index and len

### Code
```java
// Brute force solution
public String minWindow(String s, String t) {
    if (t.length() > s.length())
        return "";
    int minLen = Integer.MAX_VALUE;
    int start = 0;
    for (int i = 0; i < s.length(); i++) {
        int count = 0;
        int[] map = new int[256];
        for (char c : t.toCharArray()) {
            map[c]++;
        }
        for (int j = i; j < s.length(); j++) {
            if (map[s.charAt(j)] > 0) {
                count++;
            }
            map[s.charAt(j)]--;
            if (count == t.length()) {
                if (j - i + 1 < minLen) {
                    start = i;
                    minLen = j - i + 1;
                }
                break;
            }
        }
    }
    return minLen == Integer.MAX_VALUE ? "" : s.substring(start, start + minLen);
}
```

### Complexity
- **Time:** TLE O(n^2)
- **Space:** O(256)

---

## 🧪 Optimal Approach
### Idea
- shrinking the window once we get one substring and checking if it is still valid

### Code
```java
// optimal force solution
public String minWindow(String s, String t) {
    if (t.length() > s.length())
        return "";
    int minLen = Integer.MAX_VALUE;
    int start = 0;
    int count = 0;
    int[] map = new int[256];
    int n = s.length();
    int m = t.length();

    for (char c : t.toCharArray())
        map[c]++;
    int l = 0, r = 0;
    while (r < n) {
        if (map[s.charAt(r)] > 0) count++;
        map[s.charAt(r)]--;
        while (count == m) { // shrinking the string till it condition is valid
            if (r - l + 1 < minLen) {
                minLen = r - l + 1;
                start = l;
            }
            map[s.charAt(l)]++;
            if (map[s.charAt(l)] > 0) { // meaning we reinserted the value to the map
                count--;
            }
            l++;
        }
        r++;
    }
    return minLen == Integer.MAX_VALUE ? "" : s.substring(start, start + minLen);
}
```

### Complexity
- **Time:** O(2n) + O(m)
- **Space:** O(256)

---