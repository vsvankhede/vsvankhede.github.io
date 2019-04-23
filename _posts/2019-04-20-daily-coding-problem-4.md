---
title: 'Daily Coding Problem #4'
layout: post
---

## Linked List Cycle
Given a linked list, determine if it has a cycle in it.

Example:
```
Input: head = [2,5,0,6], pos = 1
Output: true
There is a cycle in the linked list, where tail connects to the 
second node.
```
![Imgur](https://i.imgur.com/7OeWplM.png)

## Solution
### Approach 1: Hash Table
Using a hash table we can check whether the node had been visited before.  We go through each node one by one and add it to a hash table. If the current node already exists in the hash table then return `true`. 

```java
public boolean hasCycle(ListNode head) {
	Set<ListNode> visitedNode = new HashSet<>();
	while(head != null) {
		if(visitedNode.contains(head) ) {
			return true;
		} else {
			visitedNode.add(head);
		}
		head = head.next;
	}
	return false;
}
```
#### Complexity Analysis
Time Complexity: O(N)<br/>
Space Complexity: O(N)

### Approach 2: Two Pointers
Loop through the list using two pointers fast and slow. If the list contains a cycle then it's guaranteed that the fast pointer will meet the slow pointer, otherwise fast pointer will reach to end of the list.

```java
public boolean hasCycle(ListNode head) {
	if(head == null) return false;
	
	ListNode slowPtr = head;
	ListNode fastPtr = head.next;
	
	while(slowPtr != fastPtr) {
		if(fastPtr == null || fastPtr.next == null) return false;
		slowPtr = slowPtr.next;
		fastPtr = fastPtr.next.next;
	}
	
	return true;
}
```

#### Complexity Analysis
Time Complexity: O(N)<br/>
Space Complexity: O(1)