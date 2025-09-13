# Problem: Sliding Window Maximum

## 📄 Problem Statement
array of integers nums
sliding window of size k
Return the max ele of each sliding window.
Input: nums = [1,3,-1,-3,5,3,6,7], k = 3
Output: [3,3,5,5,6,7]
Explanation:
Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       3
1 [3  -1  -3] 5  3  6  7       3
1  3 [-1  -3  5] 3  6  7       5
1  3  -1 [-3  5  3] 6  7       5
1  3  -1  -3 [5  3  6] 7       6
1  3  -1  -3  5 [3  6  7]      7

---

## 🧠 Brute Force Approach
### Idea
- slide through the k windows with two loops and find the max

### Code
```java
// Brute force solution
public int[] maxSlidingWindow(int[] nums, int k) {
    int n = nums.length;
    int[] ans = new int[n-k+1];
    for (int i = 0; i<=n-k; i++) { // till n-k, i'll have all the windows generated
        int max = nums[i];
        for (int j = i+1; j<i+k; j++) {
            max = Math.max(max, nums[j]);
        }
        ans[i] = max;
    }
    return ans;
}
```

### Complexity
- **Time:** O(n^2) or O(n-k)*O(k) TLE
- **Space:** O(n-k)

---

## 🧪 Optimal Approach
### Idea
- single traversal
- keep track of k elements / window elements
- add one, delete first from window
- to get the max, we were scanning through the loop - this is where we can use monotonic stack (here, decreasing)
- we need to use something which is open from both the end, to remove and add - so deque - double queue 
- push & pop, allowed from both back and front
- deque is for index

### Code
```java
// optimal force solution
public int[] maxSlidingWindow(int[] nums, int k) {
    int n = nums.length;
    int[] ans = new int[n-k+1];
    Deque<Integer> dq = new ArrayDeque<>();
    for (int i = 0; i<n; i++) {
        if (!dq.isEmpty() && dq.peekFirst() <= i - k) { // Remove indices outside current window
            dq.pollFirst();
        }
        while (!dq.isEmpty() && nums[dq.peekLast()] < nums[i]) {
            dq.pollLast(); // Remove smaller elements from the back
        }
        dq.offerLast(i); // add current index

        // record max when window forms
        if (i >= k - 1) {
            ans[i - k + 1] = nums[dq.peekFirst()];
        }
    }
    return ans;
}
```

### Complexity
- **Time:** O(2n) // n for traversal and n for pop back
- **Space:** O(n-k) + O(k)

---

## ✅ Key Takeaways
- greatest/smallest in constant complexity, u can try to use monotonic stack