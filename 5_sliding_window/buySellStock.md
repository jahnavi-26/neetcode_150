# Problem: Best time to Buy and Sell Stock

## 📄 Problem Statement
array prices where prices[i] is the price of a given stock on the ith day.
maximize profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.
buy has to be done before sell
Return the maximum profit, cannot achieve any profit, return 0.

---

## 🧠 Brute Force Approach
### Idea
- if we are selling on ith day, we will be buying the stock on day it has been mini before '0 to i-1'

### Code
```java
// Brute force solution
public int maxProfit(int[] prices) {
    int profit = 0; // keep track of profit
    int min = prices[0]; // mini value of stock till ith so i can buy that day
    for (int i = 1 ; i<prices.length; i++) {
        int cost = prices[i]-min; // cost of selling stock at ith day
        profit = Math.max(cost, profit);
        min = Math.min(min, prices[i]);
    }
    return profit;
}
```

### Complexity
- **Time:** O(n)
- **Space:** O(1)

---