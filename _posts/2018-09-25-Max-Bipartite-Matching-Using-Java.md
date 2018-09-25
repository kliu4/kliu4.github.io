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
public class MaxBipartiteMatching {
    public boolean dfs(int[][] graph, int i, boolean[] visited, int[] matching) {
        for (int j = 0; j < graph.length; j++) {
            if (graph[i][j] == 1 && !visited[j]) {
                visited[j] = true;
                if (matching[j] == -1 || dfs(graph, matching[j], visited, matching)) {
                    matching[i] = j;
                    matching[j] = i;
                    return true;
                }
            }
        }
        return false;
    }

    public int maxMatching(int[][] graph) {
        int n = graph.length;
        int max = 0;
        int[] matching = new int[n];
        Arrays.fill(matching, -1);
        for (int i = 0; i < n; i++) {
            if (matching[i] == -1 && dfs(graph, i, new boolean[n], matching)) {
                max++;
            }
        }
        return max;
    }

    public static void main(String[] args) {
        int[][] graph= new int[8][8];
        graph[0][4] = 1;
        graph[0][6] = 1;
        graph[1][4] = 1;
        graph[2][4] = 1;
        graph[2][5] = 1;
        graph[3][6] = 1;
        graph[3][7] = 1;
        System.out.println(new MaxBipartiteMatching().maxMatching(graph));
    }
}

```
