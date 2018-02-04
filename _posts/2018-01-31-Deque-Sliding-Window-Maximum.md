---
title: "Deque And Sliding Window Maximum"
categories:
  - Algorithm
tags:
  - Algorithm
  - Deque
---

{% include toc title="Deque And Sliding Window Maximum"" icon="file-text" %}

## Description

Deque is an useful data structure to implement stack and queue. Followings are the operations:

|         | First Element (Head) | Last Element (Tail) |
|---------|----------------------|---------------------|
| Insert  | offerFirst(e)        | offerLast(e)        |
| Remove  | pollFirst()          | pollLast()          |
| Examine | peekFirst()          | peekLast()          |

Since it implemnts stack and queue, the above operations has O(1) time complexity.

## Sliding Window Maximum

Given an array of n integer with duplicate number, and a moving window(size k), move the window at each iteration from the start of the array, find the maximum number inside the window at each moving.

## Solution

{% raw %}
```liquid
public class Solution {
	private void inDeque(Deque<Integer> deque, int num) {
		while (!deque.isEmpty() && deque.peekLast() < num) {
			deque.pollLast();
		}
		deque.offerLast(num);
	}

	private void outDeque(Deque<Integer> deque, int num) {
		if (deque.peekFirst() == num) {
			deque.pollFirst();
		}
	}

	public ArrayList<Integer> maxSlidingWindow(int[] nums, int k) {
		ArrayList<Integer> ans = new ArrayList<>();
		if (nums.length == 0 || k == 0 || nums.length < k) {
			return ans;
		}

		Deque<Integer> deque = new ArrayDeque<>();

		for (int i = 0; i < k; i++) {
			inDeque(deque, nums[i]);
		}

		ans.add(deque.peekFirst());

		for (int i = k; i < nums.length; i++) {
			inDeque(deque, nums[i]);
			outDeque(deque, nums[i - k]);
			ans.add(deque.peekFirst());
		}

		return ans;
	}
};
```
{% endraw %}
