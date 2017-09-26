---
title: "Break out BFS recursion"
categories:
  - Algorithm
tags:
  - Algorithm
  - Tree
  - Recursion
---

{% include toc title="Break out BFS recursion" icon="file-text" %}

## Introduction

Today I solved the following problem.

```
Two elements of a binary search tree (BST) are swapped by mistake.

Recover the tree without changing its structure.

Note:
A solution using O(n) space is pretty straight forward. Could you devise a constant space solution?
```

## Solution
```liquid
public class T099RecoverBST {
	private TreeNode first;
	private TreeNode second;
	
	private TreeNode smaller =  new TreeNode(Integer.MIN_VALUE);
	private TreeNode bigger =  new TreeNode(Integer.MAX_VALUE);
	
	
	public void recoverTree(TreeNode root) {
		helperTofindFirst(root);
		helperTofindSecond(root);
		swap(first, second);
	}
	
	private void swap(TreeNode first, TreeNode second) {
		int temp = first.val;
		first.val = second.val;
		second.val = temp;
	}
	
	private void helperTofindFirst(TreeNode root) {
		if(root == null)
			return;
		helperTofindFirst(root.left);
		
		if(first != null)
			return;
		if(smaller.val >= root.val)
			first = smaller;
		
		smaller = root;
		helperTofindFirst(root.right);
	}
	
	
	private void helperTofindSecond(TreeNode root) {
		if(root == null)
			return;
		helperTofindSecond(root.right);
		
		if(second != null)
			return;
		if(bigger.val <= root.val)
			second = bigger;
		
		bigger = root;
		helperTofindSecond(root.left);
	}
}
```

## Analysis  

Here, we need to break out the recursion when we find the first or second node. However, the following code doesn't break out correctly

```liquid
	private void helperTofindSecond(TreeNode root) {
		if(second != null || root == null)
			return;
		helperTofindSecond(root.right);
		
		if(bigger.val <= root.val)
			second = bigger;
		
		bigger = root;
		helperTofindSecond(root.left);
	}
```

We need to use if to check if second is null after the `helperTofindSecond(root.right);`
