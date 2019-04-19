---
title: 'Daily Coding Problem #2'
layout: post
---

## Delete Node in a Linked List
Write a function to delete a node (except the tail) in a singly linked list, given only access to that node.

Example 1:
```
Input: head = [4, 5, 1, 9], node =5
Output: [4, 1, 9]
Explanation: We are given the second node with value 5, 
the linked list should become 4 ->  1 -> 9 after calling 
delete function.
```

Note: 
* The linked list will have at least two elements.
* All of the nodes' value will be unique.
* The given node will not be the tail and it will always be the vallid node of the linked list.

## Solution
### Approach: Swap with Next Node
To delete the node from linked list we have to link the previous node with the next node of the one which we want to delete. 
Since we don't have any access to the previous node or head, we can't modify the previous node next pointer. 

We have to replace the value of node we want to delete with the value in the node after it, and then delete the node after it.
```java
class Solution {
	public void deleteNode(ListNode node) {
		ListNode nextNode = node.next;
		node.val = nextNode.val;
		node.next = nextNode.next;
		nextNode = null;
	}
}
```

##### Complexity Analysis
Time Complexity: O(1)

Space Complexity: O(1)