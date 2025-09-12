# Problem: Find Minimum in Rotated Sorted Array

## 📄 Problem Statement
the array nums = [0,1,2,4,5,6,7] might become:
[4,5,6,7,0,1,2] if it was rotated 4 times.
[0,1,2,4,5,6,7] if it was rotated 7 times.
so given this rotated sorted array, we need to find the minimum ele of the array
time complexity = O(logn)

---

## 🧠 Brute Force Approach
### Idea
- go through the array and find the minimum ele present

### Code
```java
// Brute force solution
public int[] solve(...) {
    // code here
}
```

### Complexity
- **Time:** O(n)
- **Space:** O(1)

---

## 🧪 Optimal Approach
### Idea
- bs
- now, we know that one side of mid is sorted
- if we think, the unsorted side is the one which has the rotation
- that means that's the side which is having the least ele - starting ele
- but this may or may NOT be true in some case - need to be careful abt the same
- so, pick the min from sorted (which is lo) and then eliminate the sorted part

### Code
```java
// optimal force solution
public int findMin(int[] nums) {
    int ans = Integer.MAX_VALUE;
    int lo = 0;
    int hi = nums.length - 1;
    while (lo <= hi) {
        int mid = (lo + hi) / 2;
        // check if left half is sorted
        if (nums[lo] <= nums[mid]) { // this is the sorted property
            ans = Math.min(nums[lo], ans); // lo has min value
            lo = mid+1; // eliminate sorted part
        }
        // right must be sorted if left is not
        else {
            ans = Math.min(nums[mid], ans); // mid has min value
            hi = mid-1; // eliminate sorted part
        }
    }
    return ans;
}

// further optimisation
public int findMin(int[] nums) {
    int ans = Integer.MAX_VALUE;
    int lo = 0;
    int hi = nums.length - 1;
    while (lo <= hi) {
        int mid = (lo + hi) / 2;
        // check if left half is sorted
        if (nums[lo] <= nums[hi]) { // if the current full arr is sorted
            ans = Math.min(nums[lo], ans); // no need to perform more bs
            break;
        }
        if (nums[lo] <= nums[mid]) { // this is the sorted property
            ans = Math.min(nums[lo], ans); // lo has min value
            lo = mid+1; // eliminate sorted part
        }
        // right must be sorted if left is not
        else {
            ans = Math.min(nums[mid], ans); // mid has min value
            hi = mid-1; // eliminate sorted part
        }
    }
    return ans;
}
```

### Complexity
- **Time:** O(logn) - in case of unique
- **Space:** O(1)

---

## ✅ Key Takeaways
- search+sorted = bs.