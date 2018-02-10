---
title: "TreeSet, Lambda And Sliding Window Median"
categories:
  - Algorithm
tags:
  - Algorithm
  - TreeSet
---

{% include toc title="TreeSet, Lambda And Sliding Window Median" icon="file-text" %}

## Description

TreeSet uses red-black tree to implement a Hash Tree. Similar to Priority Queue, it has O(lg(n) add, O(lg(n)) first, O(lg(n)) pollFirst. However, it has a big advantage to have O(lg(n)) remove. 

## Sliding Window Median

Given an array of n integer, and a moving window(size k), move the window at each iteration from the start of the array, find the median of the element inside the window at each moving. (If there are even numbers in the array, return the N/2-th number after sorting the element in the window. )

## Solution

{% raw %}
```liquid
public class T001 {
	public List<Integer> medianSlidingWindow(int[] nums, int k) {
		List<Integer> ans = new ArrayList<>();
		if (nums.length == 0 || k == 0 || nums.length < k) {
			return ans;
		}

		Comparator<Integer> slideComparator = (a, b) -> nums[a] != nums[b] ? nums[a] - nums[b] : a - b;
		TreeSet<Integer> minHeap = new TreeSet<>(slideComparator);
		TreeSet<Integer> maxHeap = new TreeSet<>(slideComparator.reversed());

		for (int i = 0; i < nums.length; i++) {
			if (!maxHeap.isEmpty() && nums[i] < nums[maxHeap.first()]) {
				maxHeap.add(i);
			} else {
				minHeap.add(i);
			}
			flatten(minHeap, maxHeap);
			if (minHeap.size() + maxHeap.size() == k) {
				ans.add(nums[maxHeap.first()]);
				if (minHeap.contains(i - k + 1)) {
					minHeap.remove(i - k + 1);
				} else if (maxHeap.contains(i - k + 1)) {
					maxHeap.remove(i - k + 1);
				}
			}
		}
		return ans;

	}

	private void flatten(TreeSet<Integer> minHeap, TreeSet<Integer> maxHeap) {
		while (maxHeap.size() < minHeap.size()) {
			maxHeap.add(minHeap.pollFirst());
		}
		while (maxHeap.size() > minHeap.size() + 1) {
			minHeap.add(maxHeap.pollFirst());
		}
	}
};
```
{% endraw %}
