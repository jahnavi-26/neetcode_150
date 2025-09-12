# Problem: Search in Rotated Sorted Array

## 📄 Problem Statement
the array nums = [0,1,2,4,5,6,7] might become:
[4,5,6,7,0,1,2] if it was rotated 4 times.
[0,1,2,4,5,6,7] if it was rotated 7 times.
Given the array nums after the possible rotation and an integer target,
return the 'true' of target if it is in nums, or 'false' if it is not in nums.
O(log n) runtime complexity

**all elements are not unique**

---

## 🧠 Brute Force Approach
### Idea
- Linear Search

### Code
```java
// Brute force solution
public int search(int[] nums, int target) {
    for (int i = 0; i < nums.length; i++) {
        if (nums[i] == target) return true;
    }
    return false;
}
```

### Complexity
- **Time:** O(n)
- **Space:** O(1)

---

## 🧪 Optimal Approach
### Idea

why unique quest algo doesn't work here?
example: [3,1,2,3,3,3,3], lo=0,hi=6,mid=3 -> all have value 3 -> how to compare if any r or l part is sorted?
so cant eliminate any as arr[hi]=arr[low]=arr[mid] - this is the only edge case with that algo
Better scenario -> try to trim down this condition, lo++ & hi-- -> since mid has same value

### Code
```java
// optimal force solution
public boolean search(int[] nums, int target) {
    int lo = 0;
    int hi = nums.length-1;
    while (lo<=hi) {
        int mid = (lo+hi)/2;
        if (nums[mid] == target) return true;
        // check edge case
        if (nums[mid]==nums[lo] && nums[lo]==nums[hi]) {
            lo ++;
            hi --;
            continue;
        }
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
    return false;
}
```

### Complexity
- **Time:** O(logn) - for an avg case as this is binary search
- can be O(n/2) - if we keep shrinking and shrinking the array and end up with half the size
- **Space:** O(1)

---

## ✅ Key Takeaways
- search+sorted = bs.