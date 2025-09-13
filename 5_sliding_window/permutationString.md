# Problem: Permutation in String

## 📄 Problem Statement
s2, return true if s2 contains a permutation of s1
return true if one of s1's permutations is the substring of s2
Input: s1 = "ab", s2 = "eidbaooo"
Output: true
Explanation: s2 contains one permutation of s1 ("ba").

Input: s1 = "ab", s2 = "eidboaoo"
Output: false
---

## 🧠 Brute Force Approach
### Idea
- approach is to match the frequency of element in s1 with s2's window length of s1
- store the s1 freq of char
- slide through s2 in window len of s1.length() and check if the freq matches
- since only lowercase char, we can use constant space of 26

### Code
```java
// Brute force solution
public boolean checkInclusion(String s1, String s2) {
    int[] freq = new int[26];
    for (char c : s1.toCharArray()) {
        freq[c - 'a']++; // freq of s1
    }
    int windowSize = s1.length();
    for (int i = 0; i < s2.length(); i++) {
        int[] windowfreq = new int[26]; // window freq check
        int windowIndx = 0; 
        int idx = i; 
        while (windowIndx < windowSize && idx < s2.length()) {
            windowfreq[s2.charAt(idx) - 'a']++;
            windowIndx++;
            idx++;
        }
        boolean match = true;
        for (int j = 0; j < 26; j++) {
            if (windowfreq[j] != freq[j]) {
                match = false;
                break;
            }
        }
        if (match)
            return true;
    }
    return false;
}
```

### Complexity
- **Time:** O(n^2) or (len(s1)*len(s2))
- **Space:** O(26)

---

## 🧪 Optimal Approach
### Idea
- move the window by one and remove the first char from  prev window
- edge case is when s1 is greater that s2 length

### Code
```java
// optimal force solution
public boolean checkInclusion(String s1, String s2) {
    if (s1.length() > s2.length()) return false;
    int[] freq1 = new int[26];
    int[] freq2 = new int[26];
    for (int i = 0; i<s1.length(); i++) {
        freq1[s1.charAt(i) - 'a']++; // freq of s1
        freq2[s2.charAt(i) - 'a']++; // freq of s2 char till s1 length
    }
    if (Arrays.equals(freq1, freq2)) return true; // freq check if same
    int left = 0 ; // right now, we have checked for window 0 to s1.length()-1 length
    for (int right = s1.length(); right < s2.length(); right++) {
        freq2[s2.charAt(right) - 'a']++; // move window one ahead
        freq2[s2.charAt(left) - 'a']--; // remove first char of prev window
        left ++; // move left by one for new window
        if (Arrays.equals(freq1, freq2)) return true; // check if arrays are equal
    }
    return false;
}
```

### Complexity
- **Time:** O(s1+s2)
- **Space:** O(26)

---