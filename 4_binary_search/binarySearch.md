# Problem: Binary Search

## 📄 Problem Statement
find index of a target element in given ascending sorted array, else return -1.

---

## 🧠 Brute Force Approach
### Idea
- go through each element and check if target = nums[i]
- if yes, return i
- if not found, return -1

### Code
```java
// Brute force solution
public int search(int[] nums, int target) {
    for (int i = 0; i < nums.length; i++) { // iterate the array
        if (nums[i] == target) return i; // if found, return index
    }
    return -1; // not found
}
```

### Complexity
- **Time:** O(n) - one time traversal-max the ele is at last.
- **Space:** O(1)

---

## 🧪 Optimal Approach
### Idea
- the array is SORTED
- start from middle [mid = lo + (hi-lo)/2] or [mid = (hi+lo)/2], compare - if target equals the ele, return index of mid
- if target is smaller, choose left side
- if target is greater choose right side
- again find mid, go though the process again
- if applying recursion, base condition will be found ele or l=r -> return -1

### Code
```java
// optimal force solution
public int search(int[] nums, int target) {
    int lo = 0;
    int hi = nums.length-1;
    while (lo <= hi) {
        int mid = lo + (hi-lo)/2;
        if (target == nums[mid]) return mid;
        else if (nums[mid] < target) lo = mid+1;
        else hi = mid-1;
    }
    return -1;
}
```

### Complexity
- **Time:** O(logn)
- **Space:** O(1)

---