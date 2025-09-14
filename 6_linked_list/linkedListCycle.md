# Problem: Linked List Cycle

## 📄 Problem Statement
Given head, the head of a linked list, determine if the linked list has a cycle in it.
There is a cycle in a linked list if there is some node in the list that can be reached again by continuously 
following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is 
connected to. Note that pos is not passed as a parameter.

---

## 🧠 Brute Force Approach
### Idea
- if we find mini of one node such that if we start from that node and reach back to it, 
- it means that the linked list has a cycle/loop in it
- use map here map<node, boolean> -> traverse the linked list
- check if already visited
- else add to map

### Code
```java
// Brute force solution
public boolean hasCycle(ListNode head) {
    Map<ListNode, Boolean> map = new HashMap<>();
    ListNode temp = head;
    while(temp!= null) {
        if (map.containsKey(temp)) return true;
        map.put(temp, true);
        temp = temp.next;
    }
    return false;
}
```

### Complexity
- **Time:** O(n)+2 map operations (insert and check)-> depending on map, it takes either O(2logn) or O(2*1)
- **Space:** O(n)

---

## 🧪 Optimal Approach
### Idea
- Tortoise & Hare algo -> slow and fast pointer (Floyd’s Cycle Detection Algorithm)
- two pointers, slow will be moving by 1 step and fast by 2
- if they are meeting, there is a loop in the linked list

### Code
```java
// optimal force solution
public boolean hasCycle(ListNode head) {
    ListNode slow = head;
    ListNode fast = head;
    while(fast!= null && fast.next!=null) {
        slow = slow.next;
        fast = fast.next.next;
        if (slow==fast) return true;
    }
    return false;
}
```

### Complexity
- **Time:** O(n) approx (or you can around O(n))
- **Space:** O(1)

---