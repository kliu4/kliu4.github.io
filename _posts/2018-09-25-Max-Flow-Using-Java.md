---
title: "Max Flow using Java"
categories:
  - Algorithm
tags:
  - Algorithm
  - Java
  - Max Flow
---

{% include toc title="Max Flow using Java" icon="file-text" %}

## Introduction

There are many max-flow implementations using C++, however, it is hard to find java implementation. Following is a simple implementation using java:

## Implementation

```
public class SimpleMaxFlow {

    /**
     * 1) here I don't use capacity and flow, use capacity to save updated capacity instead
     * 2) rev is the reverted edge index 
     */
    class Edge {
        int to;
        int capacity;
        int rev;

        public Edge(int to, int capacity, int rev) {
            this.to = to;
            this.capacity = capacity;
            this.rev = rev;
        }
    }

    private void addEdge(List<Edge>[] graph, int v, int w, int c) {
        graph[v].add(new Edge(w, c, graph[w].size()));
        graph[w].add(new Edge(v, 0, graph[v].size() - 1));
    }

    private int dfs(List<Edge>[] graph, boolean[] used, int v, int w, int f) {
        if (v == w) {
            return f;
        }
        used[v] = true;
        for (Edge e : graph[v]) {
            if (!used[e.to] && e.capacity > 0) {
                int d = dfs(graph, used, e.to, w, Math.min(f, e.capacity));
                if (d > 0) {
                    e.capacity -= d;
                    graph[e.to].get(e.rev).capacity += d;
                    return d;
                }
            }
        }
        return 0;
    }

    private int maxFlow(List<Edge>[] graph, int v, int w) {
        int flow = 0;
        while (true) {
            int f = dfs(graph, new boolean[graph.length], v, w, Integer.MAX_VALUE);
            if (f == 0) {
                return flow;
            }
            flow += f;
        }
    }

    public static void main(String[] args) {
        List<Edge>[] graph = new ArrayList[3];
        for (int i = 0; i < 3; i++) {
            graph[i] = new ArrayList<>();
        }
        SimpleMaxFlow simpleMaxFlow = new SimpleMaxFlow();
        simpleMaxFlow.addEdge(graph, 0, 1, 3);
        simpleMaxFlow.addEdge(graph, 0, 2, 2);
        simpleMaxFlow.addEdge(graph, 1, 2, 2);
        System.out.println(simpleMaxFlow.maxFlow(graph, 0, 2));
    }
}

```
