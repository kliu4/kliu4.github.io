---
title: "Unity3d scene doesn't show X and Y axis for my selected object"
categories:
  - Unity3d
tags:
  - Unity3d
---

{% include toc title="Unity3d scene doesn't show X and Y axis for my selected object" icon="file-text" %}

## Introduction

I have 2d objects in my 2d project. I select one of them, the unity3d scene does not show the X and Y axis. It only shows the boundingbox of my selected object as following. 

![Image of missing x and y axis](https://i.stack.imgur.com/Q5JmO.png)

## Solution

This is because my Object is a UI Object and I am in RectTransform mode since UI Objects use the RectTransform instead of just Transform. solve by chaning the model like below


![Image of missing x and y axis](https://i.stack.imgur.com/MR97A.png)
