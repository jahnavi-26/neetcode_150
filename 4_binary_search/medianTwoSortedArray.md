# Problem: Median of Two Sorted Arrays

## 📄 Problem Statement
Given two sorted arrays nums1 and nums2 of size m and n respectively, return the median of the two sorted arrays.

Time complexity - O(log (m+n)).

---

- median - equal number of ele on both the sides
- in case of odd, it will be easy but in case of even, it will be somewhere between two middle elements

## 🧠 Brute Force Approach
### Idea
- merge two sorted arrays
- then we can find median

### Code
```java
// Brute force solution
public double findMedianSortedArrays(int[] nums1, int[] nums2) {
    int n = nums1.length;
    int m = nums2.length;
    List<Integer> arr = new ArrayList<>();
    int i = 0, j = 0;
    while(i<n && j<m) {
        if (nums1[i] < nums2[j]) {
            arr.add(nums1[i]);
            i++;
        } else {
            arr.add(nums2[j]);
            j++;
        }
    }
    while (i<n) arr.add(nums1[i]);
    while (j<m) arr.add(nums2[j]);
    int len = n+m;
    if (len%2==1) return arr.get(len/2);
    else return (double)((double)arr.get(len/2) + (double)arr.get((len/2)-1))/2.0;
}
```

### Complexity
- **Time:** O(n) // need to optimise
- **Space:** O(n1+n2)

---

## 🧪 Better Approach
### Idea
- just get the len/2th ele in case of odd
- and len/, len/2 -1th ele in case of even
- no need to store all the other elements

### Code
```java
// optimal force solution
public double findMedianSortedArrays(int[] nums1, int[] nums2) {
    int n1 = nums1.length;
    int n2 = nums2.length;
    int n = n1 + n2;
    int idx1 = n / 2;
    int idx2 = n / 2 - 1;
    int idx1ele = -1;
    int idx2ele = -1;
    int i = 0, j = 0;
    int cnt = 0;
    while (i < n1 && j < n2) { 
        if (nums1[i] < nums2[j]) { // nums1[i] will be pur next ele
            if (cnt == idx1)
                idx1ele = nums1[i];
            else if (cnt == idx2)
                idx2ele = nums1[i];
            i++;
            cnt++;
        } else { // else nums2[j] will be pur next ele
            if (cnt == idx1)
                idx1ele = nums2[j];
            else if (cnt == idx2)
                idx2ele = nums2[j];
            j++;
            cnt++;
        }
    }
    while (i < n1) { // left over elements
        if (cnt == idx1)
            idx1ele = nums1[i];
        else if (cnt == idx2)
            idx2ele = nums1[i];
        i++;
        cnt++;
    }
    while (j < n2) { // left over elements
        if (cnt == idx1)
            idx1ele = nums2[j];
        else if (cnt == idx2)
            idx2ele = nums2[j];
        j++;
        cnt++;
    }
    if (n%2 == 1) return idx1ele;
    else return (double)((double) (idx1ele+idx2ele))/2.0; // typecast coz return in double
}
```

### Complexity
- **Time:** O(n1+n2)
- **Space:** O(1)

---

## 🧪 Optimal Approach
### Idea
- there is a symmetry here
- only one computation is found where all are sorted
- we need to find how many from array one should be part of the left symmetry and hwo many from the array two
- we then check if the symmetry is valid or no
- go bs on shorter array to save time - while finding symmetry

### Code
```java
// optimal force solution
public double findMedianSortedArrays(int[] nums1, int[] nums2) {
    int n1 = nums1.length;
    int n2 = nums2.length;
    if (n1 > n2) return findMedianSortedArrays(nums2, nums1);
    int low = 0, high = n1;
    int left = (n1+n2+1)/2; // ele on left of symmetry
    int n = n1+n2;
    while (low<=high) {
        int mid1 = (low+high)/2;
        int mid2 = left-mid1;
        int l1 = Integer.MIN_VALUE, l2 = Integer.MIN_VALUE; // in case they are not there
        int r1 = Integer.MAX_VALUE, r2 = Integer.MAX_VALUE;
        if (mid1<n1) r1 = nums1[mid1];
        if (mid2<n2) r2 = nums2[mid2];
        if (mid1-1 >= 0) l1 = nums1[mid1-1];
        if (mid2-1 >= 0) l2 = nums2[mid2-1];
        if (l1<=r2 && l2<=r1) {
            if (n%2 == 1) return Math.max(l1,l2);
            return (double)(Math.max(l1, l2) + Math.min(r1, r2))/2.0;
        } else if (l1>r2) high = mid1-1;
        else low = mid1+1;
    }
    return 0;
}
```

### Complexity
- **Time:** O(min (logm+logn))
- **Space:** O(1)

---