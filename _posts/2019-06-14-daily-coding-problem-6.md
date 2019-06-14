---
title: 'Daily Coding Problem #6'
layout: post
---

## Happy Number

Write an algorithm to determine if a number is "happy".
A [happy number](https://en.wikipedia.org/wiki/Happy_number) is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1(where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.

Example:
```
Input: 19
Output: true
Explanation: 
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1
```

## Solution
### Approach 1:  HashSet
Using HashSet we can maintain all the unique numbers we encounter during happy number process. In case of happy number, the process will go in the loop when the number is 1. At this point, HashSet will deny adding the duplicate number. In case of unhappy number, the process will go in a loop where during the second loop the HashSet will deny adding the duplicate number.
```java
public boolean isHappy(int num) {
	Set<Integer> uniqueNum = new HashSet<>();
	
	while(uniqueNum.add(num)) {
		int value  = 0;
		
		while(num > 0) {
			value += Math.pow(num % 10, 2);
			num /= 10;
		}
		
		num = value;
	}
	
	return num == 1;
}
```
### Approach 2: Fast Slow Pointers
We can solve this problem by using two pointers fast, slow. In a loop, the fast & slow pointer will meet each other at some point. When they meet each we can check the number where they meet. If the number is 1 then the given number is a happy number.
```java
public boolean isHappy(int num) {
	int fast, slow;
	fast = slow = num;
	
	do {
		slow = squareSum(slow);
		fast = squareSum(squareSum(fast));
	} while(fast != slow);
	
	return slow == 1;
}

private int squareSum(int num) {
	int sum = 0;
	while(num > 0) {
		sum += Math.pow(num%10 , 2);
		num /= 10;
	}
	return sum;
}
```