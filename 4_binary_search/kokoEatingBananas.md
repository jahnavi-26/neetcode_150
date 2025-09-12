# Problem: Koko eating Bananas

## 📄 Problem Statement
- n piles of bananas
- ith pile has pile[i] bananas
- koko can eat 'k' bananas in an hour
- she chooses a pile, eats k bananas (if less than k bananas in that pile, she eats all and cant eat until hour is over)
- guard is gone for 'h' hours
- find mini value of 'k' such that she eats all bananas in 'h' hours

---

## 🧠 Brute Force Approach
### Idea
- start from k=1, since that is min number of bananas koko can eat 
- calculate the hours (keep in mind, take the ceil value of pile[i]/k)
- if it is more than h, increase the value of k by one
- go through the process again
- return the first k value (will be min) where koko is able to finish all bananas in h hours
- you can also approach this by - between 1-max of the pile

### Code
```java
// Brute force solution
public int minEatingSpeed(int[] piles, int h) {
    int k = 1;
    while (true){
        int time = 0;
        for (int i = 0; i<piles.length; i++) {
            time += Math.ceil((double)piles[i]/k); // DOUBLE coz 5/2 -> auto as 2 in int the ceil of 2 will be two only
        }
        if (time<=h) break;
        k++;
    }
    return k;
}
```

### Complexity
- **Time:** TLE - O(maxele*n)
- **Space:** O(1)

---

## 🧪 Optimal Approach
### Idea
- answer always lie between 1-max of the pile
- need to find the minimum
- binary search
- lo = 1 // starts with not possible
- high = max[pile] // starts with possible always
- mid = (lo+hi)/2
- hi will end with value not possible
- lo will end where it is possible
- that's where we end the search and return lo

### Code
```java
// optimal force solution
public int minEatingSpeed(int[] piles, int h) {
    int lo = 1; // start from lo
    int hi = maxInArray(piles); // end at max of the pile
    while (lo<=hi) {
        int mid = (lo+hi)/2;
        int time = timeTaken(piles, mid); // time taken at mid
        if (time<=h) hi = mid-1; // if possible at mid, we go and find the min, so move the hi
        else lo = mid+1; // if not possible at mid, move towards hi - so move the lo
    }
    return lo;
}
public int timeTaken(int[] piles, int k) {
    int time = 0;
    for (int i = 0; i<piles.length; i++) {
        time += Math.ceil((double)piles[i]/k);
    }
    return time;
}
public int maxInArray(int[] piles) {
    int max = piles[0];
    for (int i = 1; i < piles.length; i++) {
        if (piles[i] > max) {
            max = piles[i];
        }
    }
    return max;
}
```

### Complexity
- **Time:** O(n)+O(log(maxele))
- **Space:** O(1)

---

## ✅ Key Takeaways
- binary search
- 1,  2, 3,4,5,6,7,8,9,10,11
- np,np,np,p,p,p,p,p,p,p,p
- it's between possible and not possible - that's why we choose binary search