# Problem: Merge two Sorted Lists

## 📄 Problem Statement
given the heads of two sorted linked lists list1 and list2
Merge the two lists into one sorted list
Return the head of the merged linked list
Input: list1 = [1,2,4], list2 = [1,3,4]
Output: [1,1,2,3,4,4]

---

## 🧠 Brute Force Approach
### Idea
- add the data of linked list 1 to the array
- the add the data of list 2 to the same array
- apply the sort operation on the array
- convert the sorted array to linked list
- return the head of that linked list

### Code
```java
// Brute force solution
public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
    List<Integer> arr = new ArrayList<>();
    ListNode head1 = list1;
    ListNode head2 = list2;
    while (head1!=null) {
        arr.add(head1.val);
        head1 = head1.next;
    }
    while (head2!=null) {
        arr.add(head2.val);
        head2 = head2.next;
    }
    Collections.sort(arr);
    ListNode dummy = new ListNode(0);
    ListNode curr = dummy;
    for (int val : arr) {
        curr.next = new ListNode(val);
        curr = curr.next;
    }
    return dummy.next;
}
```

### Complexity
N=n1+n2
- **Time:** O(n1)+O(n2)+O(NlogN)+O(N)
- **Space:** O(N)+O(N)

---

## 🧪 Optimal Approach
### Idea
- sorted list & two pointers

### Code
```java
// optimal force solution
public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
    ListNode t1 = list1;
    ListNode t2 = list2;
    ListNode dummy = new ListNode(0);
    ListNode temp = dummy;
    while (t1!=null && t2!=null) { // either of them is null we stop
        if (t1.val<t2.val) {
            temp.next = t1;
            temp = t1;
            t1 = t1.next;
        } else {
            temp.next = t2;
            temp = t2;
            t2 = t2.next;
        }
    }
    // if any one of these is left
    if (t1!= null) temp.next = t1;
    else temp.next = t2;
    return dummy.next;
}
```

### Complexity
- **Time:** O(n1)+O(n2)
- **Space:** O(1)

---