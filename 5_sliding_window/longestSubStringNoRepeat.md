# Problem: Longest Substring without repeating characters

## 📄 Problem Statement
Given a string s, find the length of the longest substring without duplicate characters.

**substring is consecutive, if it's not consecutive, it's a sequence**
---

## 🧠 Brute Force Approach
### Idea
- generate all the possible substrings
- keep track of longest string so far
- nbreak substring creation once duplicate is encountered

### Code
```java
// Brute force solution
public int lengthOfLongestSubstring(String s) {
    int n = s.length();
    int max = 0; // check the sub-string length
    for (int i = 0; i<n; i++) {
        StringBuilder sub = new StringBuilder(); // substring starting with char at i
        for (int j = i; j<n; j++) {
            if (sub.indexOf(String.valueOf(s.charAt(j))) != -1) { // if duplicate
                break; // as duplicate found, we would not be moving fwd with this sub-string
            } else {
                sub.append(s.charAt(j)); // add the char to sub-string
                max = Math.max(max, sub.length()); // keep updating the max len so far
            }
        }
    }
    return max;
}
```

### Complexity
- **Time:** O(n^2)
- **Space:** O(1)

---

## 🧪 Better Approach
### Idea
- Hashmap of seen alphabets - all characters are 0-255 (as per ascii values)
- 

### Code
```java
// optimal force solution
public int[] solve(...) {
    // code here
}
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## 🧪 Optimal Approach
### Idea
- Explain your optimal approach in 2–3 lines.

### Code
```java
// optimal force solution
public int[] solve(...) {
    // code here
}
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---

## ✅ Key Takeaways
- HashSet is the go-to for duplicate checks.
- Reduces O(n²) → O(n).