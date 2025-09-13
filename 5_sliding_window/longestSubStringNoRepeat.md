# Problem: Longest Substring without repeating characters

## 📄 Problem Statement
Given a string s, find the length of the longest substring without duplicate characters.

**substring is consecutive, if it's not consecutive, it's a sequence**
---

## 🧠 Brute Force Approach
### Idea
- generate all the possible substrings
- keep track of longest string so far
- break substring creation once duplicate is encountered

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

## 🧪 Brute Approach - 2
### Idea
- Hashmap of seen alphabets - all characters are 0-255 (as per ascii values)

### Code
```java
// optimal force solution
public int lengthOfLongestSubstring(String s) {
    int n = s.length();
    int max = 0; // check the sub-string length
    for (int i = 0; i<n; i++) {
        Map<Character, Integer> map = new HashMap<>();
        int len = 0;
        for (int j = i; j<n; j++) {
            if (map.containsKey(s.charAt(j))) { // if duplicate
                break; // as duplicate found, we would not be moving fwd with this sub-string
            }
            len = j-i+1; // len of substring will be j-i+1
            max = Math.max(len, max);
            map.put(s.charAt(j),1); // mark it seen
        }
    }
    return max;
}

// constant boolean variable:
public int lengthOfLongestSubstring(String s) {
    int n = s.length();
    int max = 0; // check the sub-string length
    for (int i = 0; i<n; i++) {
        boolean[] map = new boolean[256];
        int len = 0;
        for (int j = i; j<n; j++) {
            if (map[s.charAt(j)]) { // if duplicate
                break; // as duplicate found, we would not be moving fwd with this sub-string
            }
            len = j-i+1; // len of substring will be j-i+1
            max = Math.max(len, max);
            map[s.charAt(j)] = true; // mark it seen
        }
    }
    return max;
}
```

### Complexity
- **Time:** O(n^2)
- **Space:** O(256)

---

## 🧪 Optimal Approach
### Idea
- sliding window
- keep a hashmap of seen characters with their index
- l & r start from 0, move r ahead, till we encounter a char that is already seen && **it is present in the substring i.e. the map[s.charAt(r)] >= l**
- once we encounter already seen char, move pointer l to the index of repeated char+1
- keep track of the max len 

### Code
```java
// optimal force solution
public int lengthOfLongestSubstring(String s) {
    int[] lastSeen = new int[256];
    Arrays.fill(lastSeen, -1);
    int n = s.length(), max = 0, l = 0;
    for (int r = 0; r < n; r++) {
        char c = s.charAt(r);
        if (lastSeen[c] >= l) { // if seen already and is in the window
            l = lastSeen[c] + 1; // move l
        }
        lastSeen[c] = r;
        max = Math.max(max, r - l + 1);
    }
    return max;
}
```

### Complexity
- **Time:** O(n) -> just moving r
- **Space:** O(256)

---

## ✅ Key Takeaways
- when time is O(n^2), substring (max/min) -> start thinking abt two pointer & sliding window.
- these are constructive algo - not a specific algo - it keeps changing based on the problem.