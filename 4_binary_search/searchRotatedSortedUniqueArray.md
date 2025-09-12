# Problem: Search in Rotated Sorted Array

## 📄 Problem Statement
the array nums = [0,1,2,4,5,6,7] might become:
[4,5,6,7,0,1,2] if it was rotated 4 times.
[0,1,2,4,5,6,7] if it was rotated 7 times.
Given the array nums after the possible rotation and an integer target, 
return the index of target if it is in nums, or -1 if it is not in nums.
O(log n) runtime complexity

**all elements are unique**

---

## 🧠 Brute Force Approach
### Idea
- Linear Search

### Code
```java
// Brute force solution
public int search(int[] nums, int target) {
    for (int i = 0; i < nums.length; i++) {
        if (nums[i] == target) return i;
    }
    return -1;
}
```

### Complexity
- **Time:** O(n)
- **Space:** O(1)

---

## 🧪 Optimal Approach
### Idea
- use bs
- identify which half is sorted
  - check if the target is in sorted arr?
  - eliminate if not, else search in other part
- keep going

### Code
```java
// optimal force solution
public int search(int[] nums, int target) {
    int lo = 0;
    int hi = nums.length-1;
    while (lo<=hi) {
        int mid = (lo+hi)/2;
        if (nums[mid] == target) return mid;
        // check if left half is sorted
        if (nums[lo] <= nums[mid]) { // this is the sorted property
            // check if target lies in the sorted part?
            if (nums[lo] <= target && target <= nums[mid])
                hi = mid-1; // eliminate the right part
            else
                lo = mid+1; // eliminate the left part
        }
        // right must be sorted if left is not
        else {
            if (nums[mid] <= target && target <= nums[hi])
                lo = mid+1; // eliminate the left part
            else
                hi = mid-1; // eliminate the right part
        }
    }
    return -1;
}
```

### Complexity
- **Time:** O(logn)
- **Space:** O(1)

---

## ✅ Key Takeaways
- search+sorted = bs.