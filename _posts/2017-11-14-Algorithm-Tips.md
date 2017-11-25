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

## Get Digits of Positive Int

{% raw %}
```liquid
while (number > 0) {
    print( number % 10);
    number = number / 10;
}
```
{% endraw %}

## Two's Exponent

```
2^x = 1 << x;
```

## Get Kth (start form 0) binary digital

```
return (num >> k) & 1;
```

## Binary Tree's Height


```
public int height(TreeNode root){
    if(root == null)
        return 0;
    return 1 + Math.max(height(root.left), height(root.right));
}
```


## Split with Lookahead example

```
String[] strs = equation.split("(?=[+-])");
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
```

## Binary search

If the value is found, return the index; else return `-(low + 1)` while `low` is the insert position

```
private static int binarySearch0(long[] a, int fromIndex, int toIndex, long key) {
    int low = fromIndex;
    int high = toIndex - 1;

    while (low <= high) {
        int mid = (low + high) >>> 1;
        long midVal = a[mid];

        if (midVal < key)
            low = mid + 1;
        else if (midVal > key)
            high = mid - 1;
        else
            return mid; // key found
     }
   return -(low + 1);  // key not found.
}
```

## Union-Find

`Union-Find` is used to solve the nework connectivity, e.g., to check if there is cycle in set, to find disjoint sets. 

`Union` command is to conenct to sets. `Union by rank` always attaches the shorter tree to the root of the taller tree. 

`Find` command is to find the parent of a node.

```liquid
public class UnionFind {
	private int[] parent;
	private int[] size;
	private int count;

	public UnionFind(int n) {
		count = n;
		parent = new int[n];
		size = new int[n];
		for (int i = 0; i < n; i++) {
			parent[i] = i;
			size[i] = 0;
		}
	}

	public int find(int p) {
		while (p != parent[p]) {
			parent[p] = parent[parent[p]];
			p = parent[p];
		}
		return p;
	}

	public int count() {
		return count;
	}

	public boolean connected(int p, int q) {
		return find(p) == find(q);
	}

	public void union(int p, int q) {
		int rootP = find(p);
		int rootQ = find(q);
		if (rootP == rootQ)
			return;

		if (size[rootP] < size[rootQ]) {
			parent[rootP] = rootQ;
			size[rootQ] += size[rootP];
		} else {
			parent[rootQ] = rootP;
			size[rootP] += size[rootQ];
		}
		count--;
	}
}
```
