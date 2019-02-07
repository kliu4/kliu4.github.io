---
title: "Binary Indexed Tree"
categories:
  - Java
tags:
  - Java
---

{% include toc title="Binary Indexed Tree" icon="file-text" %}

## Introduction

Binary Indexed Tree using java.

## Code
```liquid
public class BIT {
    int[] sums;
    int n;

    public BIT(int n) {
        sums = new int[n];
        this.n = n;
    }

    private int lowBit(int i) {
        return i & (-i);
    }

    public void update(int i, int delta) {
        for (; i < n; i += lowBit(i)) {
            sums[i] += delta;
        }
    }

    public int query(int i) {
        int sum = 0;
        for (; i > 0; i -= lowBit(i)) {
            sum += sums[i];
        }
        return sum;
    }
}
```
