---
title: "UnionFind"
categories:
  - Algorithm
tags:
  - Algorithm
  - UnionFind
---

{% include toc title="UnionFind" icon="file-text" %}

## Description

UnionFind has two operations `union` and `find`, it could helps to operate set, e.g, find how many sets? how many elements in cell.

## Using Java and int array to implement UnionFind

{% raw %}
```liquid
public class UnionFind {
	int[] root = null;
	
	public UnionFind(int n) {
		root = new int[n + 1];
		for (int i = 0; i <= n; i++) {
			root[i] = i;
		}
	}
	
	private int find(int x) {
		if (x == root[x]) {
			return x;
		}
		
		return root[x] = find(root[x]);
	}
	
	public void union(int a, int b) {
		int rootA = find(a);
		int rootB = find(b);
		if (rootA != rootB) {
			root[rootA] = rootB;
		}
	}
}
```
{% endraw %}

## Using Java and HashMap to implement UnionFind

```
public class UnionFind {
	Map<Integer, Integer> map = new HashMap<>();
	
	public UnionFind(int n) {
		for (int i = 0; i <= n; i++) {
			map.put(i, i);
		}
	}
	
	private int find(int x) {
		if (x == map.get(x)) {
			return x;
		}
		
		map.put(x, find(map.get(x)));
		return map.get(x);
	}
	
	public void union(int a, int b) {
		int rootA = find(a);
		int rootB = find(b);
		if (rootA != rootB) {
			map.put(rootA, rootB);
		}
	}
}
```
