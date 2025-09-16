# Problem: Adding 2 Number

## 📄 Problem Statement
You are given two non-empty linked lists representing two non-negative integers. 
The digits are stored in reverse order, and each of their nodes contains a single digit. 
Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.
---

## 🧠 Brute Force Approach
### Idea
- add all the places one by one starting from the unit place
- take the carry over to next one if any

### Code
```java
// Brute force solution
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    ListNode dummy = new ListNode(-1);
    int carry = 0;
    ListNode temp1 = l1;
    ListNode temp2 = l2;
    ListNode curr = dummy;
    while (temp1 != null || temp2 != null) {
        int sum = carry;
        if (temp1!= null) sum += temp1.val;
        if (temp2!= null) sum += temp2.val;
        ListNode newNode = new ListNode(sum%10);
        carry = sum/10;
        curr.next = newNode;
        curr = curr.next;
        if (temp1!= null) temp1 = temp1.next;
        if (temp2!= null) temp2 = temp2.next;
    }
    if (carry>0) {
        ListNode newNode = new ListNode(carry);
        curr.next = newNode;
    }
    return dummy.next;
}
```

### Complexity
- **Time:** O(max(n1,n2))
- **Space:** O(max(n1,n2)) // to store the result

---