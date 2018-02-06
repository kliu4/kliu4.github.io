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

<pre>
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
</pre>

## Solution

Find max value in center row and center column (13), see bellow:

<pre>
[  
  [0,  0,  0,  0,  <i><b>0</b></i>,  0,  0,  0,  0]  
  [0, 12,  9,  3,  <i><b>4</b></i>,  5,  7,  8,  0]  
  [0, 23,  8,  2,  <i><b>3</b></i>,  9, 10,  7,  0]  
  [0, 11,  3,  2,  <i><b>8</b></i>, 14, 17,  6,  0]  
  <i><b>[0, 12,  11, 8,  7, 13,  1,  5,  0]</b></i>
  [0,  7,  16, 2,  <i><b>8</b></i>,  9, 39,  7,  0]  
  [0,  1,  8,  3,  <i><b>9</b></i>,  3, 81, 12,  0]  
  [0,  7,  9,  2,  <i><b>7</b></i>, 29, 11,  9,  0]  
  [0,  0,  0,  0,  <i><b>0</b></i>,  0,  0,  0,  0]  
]  
</pre>

Then find its four neighbors, if all are smaller than it, it is the peak element; otherwise, find a bigger element (14) and its area (the top right corner)

<pre>
[  
  [0,  0,  0,  0,  <i><b>0</b></i>,  0,  <i><b>0</b></i>,  0,  0]  
  [0, 12,  9,  3,  <i><b>4</b></i>,  5,  <i><b>7</b></i>,  8,  0]  
  [0, 23,  8,  2,  <i><b>3,  9, 10,  7,  0]</b></i>  
  [0, 11,  3,  2,  <i><b>8</b></i>, 14, <i><b>17</b></i>,  6,  0]  
  <i><b>[0, 12,  11, 8,  7, 13,  1,  5,  0]</b></i>
  [0,  7,  16, 2,  <i><b>8</b></i>,  9, 39,  7,  0]  
  [0,  1,  8,  3,  <i><b>9</b></i>,  3, 81, 12,  0]  
  [0,  7,  9,  2,  <i><b>7</b></i>, 29, 11,  9,  0]  
  [0,  0,  0,  0,  <i><b>0</b></i>,  0,  0,  0,  0]  
]  
</pre> 


Recursively to do this and find the peak element (17).

## Time Complexity
```
T(n) = T(n/4) + 2n  
     = T(n/16) + n/2 + 2n  
     = T(n/64) + n/8 + n/2 + 2n  
     = T(1) + (2 + 1/2 + 1/8 + ...)*n  
     = T(n)  
```

## Solution

{% raw %}

```liquid
public class Solution {
	public List<Integer> findPeakII(int[][] A) {
		return helper(A, 0, A.length - 1, 0, A[0].length - 1);
	}

	List<Integer> helper(int[][] A, int top, int bottom, int left, int right) {
		int midRow = top + (bottom - top) / 2;
		int midCol = left + (right - left) / 2;
		int max = A[midRow][midCol];
		int x = midRow;
		int y = midCol;

		for (int i = left; i <= right; i++) {
			if (max < A[midRow][i]) {
				max = A[midRow][i];
				y = i;
			}
		}

		for (int i = top; i <= bottom; i++) {
			if (max < A[i][midCol]) {
				max = A[i][midCol];
				x = i;
				y = midCol;
			}
		}

		int[] dx = { 1, -1, 0, 0 };
		int[] dy = { 0, 0, 1, -1 };

		for (int i = 0; i < 4; i++) {
			int newX = x + dx[i];
			int newY = y + dy[i];
			if (A[newX][newY] > max) {
				int newLeft = newX >= midCol ? midCol + 1 : left;
				int newRight = newX >= midCol ? right: midCol - 1;
				int newTop = newY >= midRow ? midRow + 1 : top;
				int newBottom = newY >= midRow ? bottom: midRow - 1;
				return helper(A, newTop, newBottom, newLeft, newRight);
			}
		}

		return Arrays.asList(x, y);
	}

	public static void main(String[] args) {
		System.out.println(new Solution().findPeakII(new int[][] { { 1, 2, 4, 3 }, { 5, 6, 8, 7 }, { 9, 10, 12, 11 },
				{ 13, 14, 16, 15 }, { 21, 22, 24, 23 }, { 17, 18, 20, 19 } }));
	}
};
```
{% endraw %}
