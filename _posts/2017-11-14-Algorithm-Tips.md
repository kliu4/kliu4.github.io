---
title: "Algorithm Tips"
categories:
  - Algorithm
tags:
  - Algorithm
---

{% include toc title="Algorithm Tips" icon="file-text" %}

## Great Common Divisor

Euclid Algorithm is the most famous algorithm for the GCD.

{% raw %}
```liquid
int generateGCD(int a,int b){
     if (b == 0) return a;
     return generateGCD(b, a % b);
}
```
{% endraw %}

## Two's Exponent

```
2^x = 1 << x;
```

## Binary Tree's Height


```
public int height(TreeNode root){
    if(root == null)
        return 0;
    return 1 + Math.max(height(root.left), height(root.right));
}
```


## Naive Tree BFS

```
public void breadth(TreeNode root) {
    if (root == null)
        return;
    Queue<TreeNode> queue = new LinkedList<BinaryTree.TreeNode>() ;
    queue.offer(root);
    while(!queue.isEmpty()){
        TreeNode node = queue.poll();
        // Add your handle functions here, e.g.,  System.out.print(node.element + " ");
        if(node.left != null) queue.offer(node.left);
        if(node.right != null) queue.offer(node.right);
    }
}
```
