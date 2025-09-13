# Problem: Longest Repeating Character Replacement

## 📄 Problem Statement
given a string s, & integer, replacement of any character is allowed - only k times
return len of longest substring having all char as equals
Example 1:

Input: s = "ABAB", k = 2
Output: 4
Explanation: Replace the two 'A's with two 'B's or vice versa.
Example 2:

Input: s = "AABABBA", k = 1
Output: 4
Explanation: Replace the one 'A' in the middle with 'B' and form "AABBBBA".
The substring "BBBB" has the longest repeating letters, which is 4.
There may exists other ways to achieve this answer too.

---

## 🧠 Brute Force Approach
### Idea
- generate all the substrings
- we try to convert the char which are lesser in count
- formula : length - max_freq -> no of char I need to change
- hash/array of 26 upper case characters to find the max frequency
- 

### Code
```java
// Brute force solution
public int characterReplacement(String s, int k) {
    int n = s.length();
    int maxLen = 0;
    for (int i = 0; i<n; i++) {
        int[] count = new int[26]; // keep frequency of the characters
        int maxFreq = 0;
        for (int j = i; j<n; j++) {
            count[s.charAt(j)-'A']++; // increase char frequency
            maxFreq = Math.max(maxFreq, count[s.charAt(j)-'A']); // update maxfreq
            int changes = j-i+1 - maxFreq; // no. of replacements = length - maxfreq
            if (changes<=k) maxLen = Math.max(maxLen, j-i+1); // check if the changes are within k limit, if yes, max len can be updated
            else break; // if not, we have crossed the k limit - break the loop
        }
    }
    return maxLen;
}
```

### Complexity
- **Time:** O(n^2) // got TLE
- **Space:** O(26)

---

## 🧪 Better Approach
### Idea
- two pointer & sliding window
- keep map of the character frequency
- trim down the window when the changes exceed the value k

### Code
```java
// better solution
public int characterReplacement(String s, int k) {
    int n = s.length();
    int maxLen = 0;
    int l = 0;
    int[] count = new int[26];
    int maxfreq = 0;
    for (int r = 0; r < n; r++) {
        count[s.charAt(r)-'A']++; // update the found char's freq
        maxfreq = Math.max(maxfreq, count[s.charAt(r)-'A']); // update max freq
        while (r-l+1-maxfreq > k) { // if this substring is not valid one, we trim it down
            count[s.charAt(l)-'A']--; // decrease the count
            for (int i=0; i<26; i++) {
                maxfreq = Math.max(maxfreq, count[i]); // update the max freq change
            }
            l++; // keep trimming the substring
        }
        if ((r-l+1)-maxfreq <= k) maxLen = Math.max(maxLen, r-l+1); // update the max len if the substring is valid
    }
    return maxLen;
}
```

### Complexity
- **Time:** O{[n(outside)+n(inner loop)]*26(for each)} -> can be optimised more // O(2N)
- **Space:** O(26)

---

## 🧪 Optimal Approach
### Idea
- in the above solution:
- no need to update the max freq while trimming down
  - why? -> because maxlen is already set on max of what we found so far, we would not want to decrease it
- still takes O(2N)
- the second while loop is trimming the substring, can be done with if as it won't let it do beyond if condition doesn't satisfy

### Code
```java
// optimal force solution
public int characterReplacement(String s, int k) {
    int n = s.length();
    int maxLen = 0;
    int l = 0;
    int[] count = new int[26];
    int maxfreq = 0;
    for (int r = 0; r < n; r++) {
        count[s.charAt(r)-'A']++;
        maxfreq = Math.max(maxfreq, count[s.charAt(r)-'A']);
        if (r-l+1-maxfreq > k) { // if this substring is not valid one, we trim it down
            count[s.charAt(l)-'A']--;
            l++;
        }
        if ((r-l+1)-maxfreq <= k) maxLen = Math.max(maxLen, r-l+1);
    }
    return maxLen;
}
```

### Complexity
- **Time:** O(N)
- **Space:** O(26)

---