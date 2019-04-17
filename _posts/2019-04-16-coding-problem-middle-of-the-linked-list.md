---
title: 'Daily Coding Problem #1'
layout: post
---

## Middle of the Linked List
Given a non-empty, singly linked list with head node `head`, return a middle node of linked list.  If there are two middle nodes, return the second middle node.

For example, given the following linked list.

Example 1:
```
Input [1, 2, 3, 4, 5]
Outout: Node 3 from this list.
```
Example 2:
```
Input: [1,2,3,4,5,6]
Outout: Node 4 from this list
```

## Solution
### Approach 1: Calculate list size
Traverse list from head to tail, and count the number nodes in the linked list. Then find the mid of list using list size which is `size/2`. Traverse list again from head to the midpoint and return middle node.

```java
class Solution {
	public ListNode middleNode(ListNode head) {
		ListNode d = head;
		int size = 1;
		while(d.next != null) {
			d = d.next;
			size++;
		}
		
		int mid = size/2;
		ListNode midNode = head;
		
		for(int i = 1; i <= mid; i++) {
			midNode = midNode.next;
		}
		
		return midNode;
	}
}
```

##### Complexity Analysis
* Time Complexity: O(N), where N is the number of nodes in the given list.
* Space Complexity: O(1), the space used by int and ListNode variables.

### Approach 2: Fast and Slow Poniter
Traverse list with two pointers slow and fast. Fast pointer traverses twice as fast then slow. When the fast pointer reaches the end of the list, the slow pointer must be in the middle.

```java
class Solution {
	public ListNode middleNode(ListNode head) {
		ListNode fast = head;
		ListNode slow = head;
		while(fast != null && fast.next != null) {
			slow = slow.next;
			fast = fast.next.next;
		}
		return slow;
	}
}
```

##### Complexity Analysis
* Time Complexity: O(N), where N is the number of nodes in the given list.
* Space Complexity: O(1), the space used by slow and fast.