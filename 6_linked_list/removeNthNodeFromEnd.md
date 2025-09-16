# Problem: Remove Nth node from the end of the List

## 📄 Problem Statement
Given the head of a linked list, 
remove the nth node from the end of the list and return its head

---

## 🧠 Brute Force Approach
### Idea
- we find the len if the LL
- reach the len-n node and change the pointer of that node to next's

### Code
```java
// Brute force solution
public ListNode removeNthFromEnd(ListNode head, int n) {
    int len = 0;
    ListNode temp = head;
    while (temp != null) {
        len ++;
        temp = temp.next;
    }
    if (len == n) {
        return head.next;
    }
    int res = len-n;
    temp = head;
    while (temp != null) {
        res--;
        if (res == 0) break;
        temp = temp.next;
    }
    temp.next = temp.next.next;
    return head;
}
```

### Complexity
- **Time:** O(len) + O(len-n) -> O(2N)
- **Space:** O(1)

---

## 🧪 Optimal Approach
### Idea
- fast and slow pointer approach
- if n=2, move the fast pointer to two (don't move slow pointer)
- then next step will be to move them together by 1
- when fast reach last node, slow will be pointing to the len-n node

### Code
```java
// optimal force solution
public ListNode removeNthFromEnd(ListNode head, int n) {
    ListNode fast = head;
    ListNode slow = head;
    for (int i = 0; i<n; i++) {
        fast = fast.next;
    }
    if (fast == null) return head.next;
    while (fast.next!=null) {
        slow = slow.next;
        fast = fast.next;
    }
    slow.next = slow.next.next;
    return head;
}
```

### Complexity
- **Time:** O(len)
- **Space:** O(1)

---