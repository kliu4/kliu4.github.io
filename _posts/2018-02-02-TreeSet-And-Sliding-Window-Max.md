---
title: "Deque And Sliding Window Max"
categories:
  - Algorithm
tags:
  - Algorithm
  - Deque
---

{% include toc title="Deque And Sliding Window Max" icon="file-text" %}

## Description

Deque is an useful data structure to implement stack and queue. Followings are the operations:

Insert: offerFirst(e), offerLast(e)  
Remove: pollFirst(), pollLast()  
Examine: peekFirst(), peekLast()  

Since it implemnts stack and queue, the above operations has O(1) time complexity.

## Sliding Window Median

Given an array of n integer, and a moving window(size k), move the window at each iteration from the start of the array, find the median of the element inside the window at each moving. (If there are even numbers in the array, return the N/2-th number after sorting the element in the window. )

## Solution

{% raw %}
```liquid
public class Solution {
    class Node {
        int id;
        int val;
        Node(int id, int val) {
            this.id = id;
            this.val = val;
        }
    }
    
    class NodeComparator implements Comparator<Node> {
        @Override
        public int compare(Node node1, Node node2) {
            return node1.val == node2.val ? node1.id - node2.id : node1.val - node2.val;
        }
    }
    
    
    public List<Integer> medianSlidingWindow(int[] nums, int k) {
        // write your code here
        int n = nums.length;
        TreeSet<Node> minheap = new TreeSet<Node>(new NodeComparator());
        TreeSet<Node> maxheap = new TreeSet<Node>(new NodeComparator().reversed());
        ArrayList<Integer> result = new ArrayList<Integer> ();
        
        if (k == 0)
            return result;
        
        Node[] nodes = new Node[nums.length];
        
        for (int i = 0; i < nums.length; i++) {
            nodes[i] = new Node(i, nums[i]);
        }
        
        Node median = nodes[0];
        
        for (int i = 1; i < k; i++) {
            Node node = nodes[i];
            median = add(minheap, maxheap, median, node);
        }
        
        result.add(median.val);
        
        for (int i = k; i < nums.length; i++) {
            Node node = nodes[i];
            median = add(minheap, maxheap, median, node);
            median = remove(minheap, maxheap, median, nodes[i - k]);
            result.add(median.val);
        }
        return result;
    }
    
    private Node flatten(TreeSet<Node>minheap, TreeSet<Node> maxheap, Node median) {
        while (minheap.size() > maxheap.size() + 1) {
            maxheap.add(median);
            median = minheap.pollFirst();
        }
        while (minheap.size() < maxheap.size()) {
            minheap.add(median);
            median = maxheap.pollFirst();
        }
        return median;
    }
    
    private Node add(TreeSet<Node>minheap, TreeSet<Node> maxheap, Node median, Node node) {
        if (median.val < node.val) {
            minheap.add(node);
        } else {
            maxheap.add(node);
        }
        return flatten(minheap, maxheap, median);
    }
    
    private Node remove(TreeSet<Node> minheap, TreeSet<Node> maxheap, Node median, Node node) {
		if(minheap.contains(node)) {
			minheap.remove(node);
		} else if (median == node){
			median = minheap.isEmpty() ? maxheap.pollFirst() : minheap.pollFirst();
		} else {
			maxheap.remove(node);
		} 
		
		return flatten(minheap, maxheap, median);
	}
}
```
{% endraw %}
