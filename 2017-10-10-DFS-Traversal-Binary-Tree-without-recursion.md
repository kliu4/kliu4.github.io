---
title: "DFS Traversal Binary Tree without Recurrsion"
categories:
  - Algorithm
tags:
  - Algorithm
  - Tree
  - Recursion
---

{% include toc title="DFS Traversal Binary Tree without Recurrsion" icon="file-text" %}

## Introduction

DFS is the basic traversal solution of the binary tree. Normally it is easy to use the recurrsion to solve the DFS. However, interative also could work for DFS

## Solution

### PostOrder
```liquid
	public List<Integer> postorderTraversal(TreeNode root) {
		List<Integer> list = new ArrayList<>();
		Stack<TreeNode> s1 = new Stack<>();
		if(root == null)
			return list;
		s1.push(root);
		while(!s1.isEmpty() && root != null) {
			TreeNode temp1 = s1.pop();
			if(temp1.left != null)
				s1.push(temp1.left);
			if(temp1.right != null)
				s1.push(temp1.right);
			
			list.add(0, temp1.val);
		}
		
		return list;
	}
```
