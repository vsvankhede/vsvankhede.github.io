---
title: 'Daily Coding Problem #3'
layout: post
---

## Merge Two Sorted Linked Lists
Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

Example:

```
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```

## Solution
### Approach 1: Using Dummy Node
We can solve this problem using a dummy node with the pointer `tail`. Dummy node gives the starting point for the result list. The `tail` pointer always points to the last node of the result list. Loop through lists and add a node from list to `tail`. When we are done return the resulting `dummy.next`.

```java
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if(l1 == null) return l2;
        if(l2 == null) return l1;
        
        
        ListNode dummy = new ListNode(0);
        ListNode tail = dummy;
        
        while (l1 != null && l2 != null) {
            if(l1.val < l2.val) {
                tail.next = l1;
                l1 = l1.next;
            } else {
                tail.next = l2;
                l2 = l2.next;   
            }
            tail = tail.next;
        }
        
        if(l1 == null) tail.next = l2;
        if(l2 == null) tail.next = l1;
        
        return dummy.next;
    }
}
```
##### Complexity Analysis
Time Complexity: O(N)
Space Complexity: O(1)

### Approach 2: Using Recursion
We can solve this problem using recursion as well. Though this solution is not recommended as this recursive solution uses extra space proportional to list length.

```java
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {      
        
        if(l1 == null) return l2;
        if(l2 == null) return l1;
        
        ListNode temp;
        
        if(l1.val <= l2.val) {
            temp = l1;
            temp.next = mergeTwoLists(l1.next, l2);
        } else {
            temp = l2;
            temp.next = mergeTwoLists(l1, l2.next);
        }
        
        return temp;
    }
}
```
##### Complexity Analysis
Time Complexity: O(N)
Space Complexity: O(N)





Reference: [Leetcode](https://leetcode.com/problems/merge-two-sorted-lists/)