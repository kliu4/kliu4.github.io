---
title: "Backtracking"
categories:
  - Algorithm
tags:
  - Backtracking
---

{% include toc title="Backtracking" icon="file-text" %}

## Introduction

Backtracking is the algorithm for finding all (or some) solutions to some __constraint satisfaction problems__, that incrementally __builds candidates__ to the solutions, and __abandons__ each partial candidate ("backtracks") as soon as it determines that the candidate cannot possibly be completed to a valid solution[1].

Backtracking tries all posible options Whenever the algorithm needs to decide between multiple options.

## Example

Suppose there are three roads (road A, B, C) in front of you and you want to find all the solutions to destination D. Backtracking tries road A first and finds it is a solution; then return to the original position and tries road B and finds it is not a solution; then return to the original position again and tries the road c and finds it is a solution. At last the backtracking could give the results (road A and C).

## Reference
1: https://en.wikipedia.org/wiki/Backtracking