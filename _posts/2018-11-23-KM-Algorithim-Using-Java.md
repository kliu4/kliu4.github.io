---
title: "Max Weight Bipartite Matching using Java"
categories:
  - Algorithm
tags:
  - Algorithm
  - Java
---

{% include toc title="Max Weight Bipartite Matching using Java" icon="file-text" %}

```
import java.util.Arrays;

public class KM {
    int n;
    int m;
    int[] x;
    int[] y;
    int[] link;
    int[][] grid;
    int[] slack;
    boolean[] visx;
    boolean[] visy;

    public int km(int[][] grid) {
        this.grid = grid;
        n = grid.length;
        m = grid[0].length;
        x = new int[n];
        y = new int[m];
        link = new int[m];
        slack = new int[m];
        Arrays.fill(link, -1);
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                x[i] = Math.max(x[i], grid[i][j]);
            }
        }

        for (int i = 0; i < n; i++) {
            Arrays.fill(slack, Integer.MAX_VALUE);

            while (true) {
                visx = new boolean[n];
                visy = new boolean[m];
                if (dfs(i)) {
                    break;
                }
                int d = Integer.MAX_VALUE;
                for (int j = 0; j < m; j++) {
                    if (!visy[j])
                        d = Math.min(d, slack[j]);
                }
                for (int j = 0; j < n; j++)
                    if (visx[j]) x[j] -= d;
                for (int j = 0; j < m; j++)
                    if (visy[j]) y[j] += d;
                    else slack[j] -= d;
            }
        }
        int sum = 0;
        for (int i = 0; i < m; i++) {
            sum += grid[link[i]][i];
        }

        return sum;
    }

    private boolean dfs(int i) {
        visx[i] = true;
        for (int j = 0; j < m; j++) {
            if (visy[j]) continue;
            int d = x[i] + y[j] - grid[i][j];
            if (d == 0 ) {
                visy[j] = true;
                if (link[j] == -1 || dfs(link[j])) {
                    link[j] = i;
                    return true;
                }
            }
            slack[j] = Math.min(slack[j], d);
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
        System.out.println(new KM().km(graph));
    }
}

```
