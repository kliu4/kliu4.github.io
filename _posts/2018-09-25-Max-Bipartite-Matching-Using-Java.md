---
title: "Max Bipartite Matching using Java"
categories:
  - Algorithm
tags:
  - Algorithm
  - Java
  - Max Bipartite Matching
---

{% include toc title="Max Bipartite Matching using Java" icon="file-text" %}

## Introduction

There are many max-Bipartite-Matching implementations using C++, however, it is hard to find java implementation. Following is a simple implementation using java:

## Implementation

```
import java.util.Arrays;

public class MaxMatch {
    int n;
    int m;
    int[][] grid;
    int[] link;
    boolean[] vis;

    public int hungraian(int[][] grid) {
        n = grid.length;
        m = grid[0].length;
        link = new int[m];
        this.grid = grid;
        Arrays.fill(link, -1);
        int count = 0;

        for (int i = 0; i < n; i++) {
            vis = new boolean[m];
            if (dfs(i)) {
                count++;
            }
        }
        return count;
    }

    private boolean dfs(int i) {
        for (int j = 0; j < m; j++) {
            if (vis[j] || grid[i][j] != 1) {
                continue;
            }
            vis[j] = true;
            if (link[j] == -1 || dfs(link[j])) {
                link[j] = i;
                return true;
            }
        }
        return false;
    }

    public static void main(String[] args) {
        int[][] graph= new int[4][4];
        graph[0][0] = 1;
        graph[0][2] = 1;
        graph[1][0] = 1;
        graph[2][0] = 1;
        graph[2][1] = 1;
        graph[3][2] = 1;
        graph[3][3] = 1;
        System.out.println(new MaxMatch().hungraian(graph));
    }
}

```
