---
title: "Great Common Divisor"
categories:
  - Algorithm
tags:
  - Algorithm
---

{% include toc title="Great Common Divisor" icon="file-text" %}

## Introduction

Euclid Algorithm is the most famous algorithm for the GCD.

```
gcd(a, 0) = a
gcd(0, b) = b
gcd(a, b) = gcd(b, a % b)
```

## Solution

{% raw %}
```liquid
int generateGCD(int a,int b){
     if (b == 0) return a;
     return generateGCD(b, a % b);
}
```
{% endraw %}
