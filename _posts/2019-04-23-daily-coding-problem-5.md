---
title: 'Daily Coding Problem #5'
layout: post
---

## Palindrome Linked List
Given a singly linked list, determine if it is a palindrome.

Example 1:

```
Input: 1->2
Output: false
```

Example 2:

```
Input: 1->2->2->1
Output: false
```

## Solution
### Approach 1:  Reverse List
Create a new list in reverse order then compare each node of both lists. 

```java
public boolean isPalindrome(ListNode head) {
	if(head == null || head.next == null) return true;

	ListNode aux = new ListNode(head.val);
	ListNode tmp = head;
	
	while(tmp.next != null) {
		ListNode d = new ListNode(tmp.next.val);
		d.next = aux;
		aux = d;
		tmp = tmp.next;
	}
	
	tmp = head;
	while(aux != null) {
		if(aux.val != tmp.val) return false;
		aux = aux.next;
		tmp = tmp.next;
	}
	
	
	return true;
}
```

#### Complexity Analysis
Time Complexity: O(N + N) ~O(N)<br/>
Space Complexity: O(N)

### Approach 2: Break and reverse second half
Break the input list into two equal sublists. Then reverse the second list and compare it with the first list.  Use two pointers fast and slow to get the middle node of the list.

```java
public boolean isPalindrome(ListNode head) {
	if(head == null || head.next == null) {
		return true;
	}
	
	ListNode fast = head;
	ListNode slow = head;
	
	while(fast.next != null && fast.next.next != null) {
		slow = slow.next;
		fast = fast.next.next;
	}
	
	ListNode secondHead = slow.next;
	slow.next = null;
	
	// Reverse second part of the list
	ListNode p1 = secondHead;
	ListNode p2 = p1.next;
	while(p2 != null) {
		ListNode tmp = p2.next;
		p2.next  = p1;
		p1 = p2;
		p2 = tmp;
	}
	
	secondHead.next = null;
	
	ListNode p = p1;
	ListNode q = head;
	while(p != null) {
		if(p.val != q.val) return false;
		p = p.next;
		q = q.next;
	}
	
	return true;
}
```

#### Complexity Analysis
Time Complexity: O(N)<br/>
Space Complexity: O(1)