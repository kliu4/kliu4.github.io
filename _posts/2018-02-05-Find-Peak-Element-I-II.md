---
title: "Using Binary Search to find peak element I, II"
categories:
  - Algorithm
tags:
  - Algorithm
  - Deque
---

{% include toc title="Using Binary Search to find peak element I, II" icon="file-text" %}

## Description

Find peak Element I is very easy, using the naive binary search could solve it. 

For the Find peak Element II, it is to ask to find peak element in 2d array, e.g, to find peak elements in following table.

[  
  [0,  0,  0,  0,  0,  0,  0,  0,  0]  
  [0, 12,  9,  3,  4,  5,  7,  8,  0]  
  [0, 23,  8,  2,  3,  9, 10,  7,  0]  
  [0, 11,  3,  2,  8, 14, 17,  6,  0]  
  [0, 12,  11, 8,  7, 13,  1,  5,  0]  
  [0,  7,  16, 2,  8,  9, 39,  7,  0]  
  [0,  1,  8,  3,  9,  3, 81, 12,  0]  
  [0,  7,  9,  2,  7, 29, 11,  9,  0]  
  [0,  0,  0,  0,  0,  0,  0,  0,  0]  
]  

## Solution

Find max value in center row and center column (13), see bellow:

[  
  [0,  0,  0,  0,  **0**,  0,  0,  0,  0]  
  [0, 12,  9,  3,  **4**,  5,  7,  8,  0]  
  [0, 23,  8,  2,  **3**,  9, 10,  7,  0]  
  [0, 11,  3,  2,  **8**, 14, 17,  6,  0]  
  **[0, 12,  11, 8,  7, 13,  1,  5,  0]**  
  [0,  7,  16, 2,  **8**,  9, 39,  7,  0]  
  [0,  1,  8,  3,  **9**,  3, 81, 12,  0]  
  [0,  7,  9,  2,  **7**, 29, 11,  9,  0]  
  [0,  0,  0,  0,  **0**,  0,  0,  0,  0]  
]  

Then find its four neighbors, if all are smaller than it, it is the peak element; otherwise, find a bigger element (14) and its area (the top right corner)

[  
  [0,  0,  0,  0,  **0**,  0,  **0**,  0,  0]  
  [0, 12,  9,  3,  **4**,  5,  **7**,  8,  0]  
  [0, 23,  8,  2,  **3,  9, 10,  7,  0]**  
  [0, 11,  3,  2,  **8**, 14, **17**,  6,  0]  
  **[0, 12,  11, 8,  7, 13,  1,  5,  0]**  
  [0,  7,  16, 2,  **8**,  9, 39,  7,  0]  
  [0,  1,  8,  3,  **9**,  3, 81, 12,  0]  
  [0,  7,  9,  2,  **7**, 29, 11,  9,  0]  
  [0,  0,  0,  0,  **0**,  0,  0,  0,  0]  
]  

Recursively to do this and find the peak element.

## Time Complexity

T(n) = T(n/4) + 2n = T(n/16) + n/2 + 2n = T(n/64) + n/8 + n/2 + 2n
     = T(1) + (2 + 1/2 + 1/8 + ...)*n
     = T(n)

{% raw %}
```liquid

```
{% endraw %}
