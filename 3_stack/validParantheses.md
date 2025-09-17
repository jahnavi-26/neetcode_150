# Problem: Valid Parantheses

## 📄 Problem Statement
Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.
Input: s = "()[]{}"
Output: true

Input: s = "(]"
Output: false
---

## 🧠 Brute Force Approach
### Idea
- Need to check the last opening bracket

### Code
```java
// Brute force solution
public boolean isValid(String s) {
    Stack<Character> stack = new Stack<>();
    for (char ch : s.toCharArray()) {
        if (ch == '(' || ch == '[' || ch == '{') stack.push(ch);
        else {
            if (stack.isEmpty()) return false;
            char top = stack.pop();
            if (ch == ')' && top != '(') return false;
            if (ch == ']' && top != '[') return false;
            if (ch == '}' && top != '{') return false;
        }
    }
    return stack.isEmpty();
}
```

### Complexity
- **Time:** O(n)
- **Space:** O(n)

---