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
public void bfs(TreeNode root) {
    Queue<TreeNode> queue = new LinkedList<TreeNode>() ;
    queue.offer(root);
    while(!queue.isEmpty()){
        TreeNode node = queue.poll();
        // Do your business here, e.g.,  System.out.print(node.element + " ");
        if(node.left != null) queue.offer(node.left);
        if(node.right != null) queue.offer(node.right);
    }
}
```

## Naive Tree Level Order BFS

```
public void levelBfs(TreeNode root) {
    Queue<TreeNode> queue = new LinkedList<TreeNode>();
    queue.add(root);
    while(!queue.isEmpty()){
        int size = queue.size();
        for(int i = 0; i < size; i++){
            TreeNode node = queue.poll();
            //Do your business
            if(node.left != null) queue.offer(node.left);
            if(node.right != null) queue.offer(node.right);
        }
       //Do your business
    }
}
```
## Get Top 3 elements in O(n) time

```
public int[] top3(int[] nums) {
    int max1 = Integer.MIN_VALUE;
    int max2 = Integer.MIN_VALUE;
    int max3 = Integer.MIN_VALUE;
        
    for(int num:nums){
        if(num > max1){
            max3 = max2;
            max2 = max1;
            max1 = num;
        }else if (num > max2){
            max3 = max2;
            max2 = num;
        }else if (num > max3){
            max3 = num;
        }
    }
    return new int[]{max3, max2, max1};
}
