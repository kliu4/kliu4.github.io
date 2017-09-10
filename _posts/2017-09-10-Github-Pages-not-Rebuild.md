---
title: "Github Pages not Rebuild"
categories:
  - Github
tags:
  - Github, Minimum-Mistakes, Jekyll
---

{% include toc title="Github Pages not Rebuild" icon="file-text" %}

## Introduction

Today, I added a new post about graph. But the Github Pages did not automatically rebuild after I change the contenct. Eventhough, I deleted that post, it still did not rebuild. 

## Solution

* "Cut" the content of index.html and commit.   
* Then it will rebuild.   
* Then copy the content back to index.html and it will conduct another rebuiding. 
