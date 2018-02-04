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

Insert: offerFirst(e), offerLast(e)  
Remove: pollFirst(), pollLast()  
Examine: peekFirst(), peekLast()  

Since it implemnts stack and queue, the above operations has O(1) time complexity.

## Sliding Window Maximum

Given an array of n integer with duplicate number, and a moving window(size k), move the window at each iteration from the start of the array, find the maximum number inside the window at each moving.


