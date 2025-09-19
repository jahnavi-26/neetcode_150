# Problem: Min Stack

## 📄 Problem Statement
Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.
["MinStack","push","push","push","getMin","pop","top","getMin"]
[[],[-2],[0],[-3],[],[],[],[]]
Output
[null,null,null,null,-3,null,0,-2]
---

## 🧠 Brute Force Approach
### Idea
- if we integrate through the stack to find the min, it will take O(n)
- store in stack as a pair<val, min till now>

### Code
```java
// Brute force solution
class MinStack {
    private Stack<int[]> st;

    public MinStack() {
        st = new Stack<>();
    }

    public void push(int val) {
        if (st.isEmpty())
            st.push(new int[] { val, val });
        else {
            int currMin = st.peek()[1];
            st.push(new int[] { val, Math.min(val, currMin) });
        }
    }

    public void pop() {
        if (!st.isEmpty()) {
            st.pop();
        }
    }

    public int top() {
        return st.peek()[0];
    }

    public int getMin() {
        return st.peek()[1];
    }
}
```

### Complexity
- **Time:** O(1)
- **Space:** O(2n) - array // need to optimise this

---

## 🧪 Optimal Approach
### Idea
- keep a min value - whenever you modify this value, (replace it with min) - it is going to be our top value
- push to stack a computed value, it's easy to go back to prev min value, 2 x val-prev min = newVal
- 

### Code
```java
// optimal force solution
class MinStack {
    private Stack<Long> st;
    long min;

    public MinStack() {
        st = new Stack<>();
    }

    public void push(int val) {
        if (st.isEmpty()) {
            st.push((long) val);
            min = (long)val;
        } else if (val < min) {
            st.push(2L * val - min);
            min = (long)val;
        } else {
            st.push((long) val);
        }
    }

    public void pop() {
        long t = st.pop();
        if (t < min) { // we have altered the value and inserted
            min = 2 * min - t;
        }
    }

    public int top() {
        long t = st.peek();
        return t < min ? (int) min : (int) t;
    }

    public int getMin() {
        return (int) min;
    }
}

```

### Complexity
- **Time:** O(1)
- **Space:** O(n)

---