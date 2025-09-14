# Problem: Reverse Linked List

## 📄 Problem Statement
Given the head of a singly linked list, reverse the list, and return the reversed list head.

---

## 🧠 Brute Force Approach
### Idea
- use stack, to store the data of linked list
- stack coz we need to reverse and it is last in first out
- iterate the linked list once, populate the stack
- again iterate and replace the data of linked list from top of stack

### Code
```java
// Brute force solution
public ListNode reverseList(ListNode head) {
    // 2 Pass algo
    // store the val
    ListNode temp = head;
    Stack<Integer> st = new Stack<>();
    while (temp!=null) {
        st.push(temp.val);
        temp = temp.next;
    }

    // pop from stack and reverse the linked list
    temp = head;
    while(temp!=null) {
        temp.val = st.peek();
        st.pop();
        temp = temp.next;
    }

    return head;
}
```

### Complexity
- **Time:** O(2n)
- **Space:** O(n) // optimise this

---

## 🧪 Optimal Approach
### Idea
- keep the data of linked list intact
- need to make the mext point in backward direction (opposite)

### Code
```java
// optimal force solution
public ListNode reverseList(ListNode head) {
    ListNode prev = null;
    ListNode temp = head;
    while (temp!=null) {
        ListNode front = temp.next; // front node of current temp
        temp.next = prev; // temp should point to prev
        prev = temp; // prev should move one ahead
        temp = front; // and temp should also move one ahead
    }
    return prev;
}

// recursive solution
public ListNode reverseList(ListNode head) {
    return reverse(head);
}

public ListNode reverse(ListNode head) {
    // for null list or one node
    if (head == null || head.next == null) return head;
    // for more than one node, we need to make it as sub problem 
    // each sub problem will be returning the head of reverse linked list
    ListNode newHead = reverse(head.next);
    ListNode front = head.next;
    front.next = head;
    head.next = null;
    return newHead;
}
```

### Complexity
- **Time:** O(n)
- **Space:** O(1) & in recursion - O(n) // recursive stack space

---