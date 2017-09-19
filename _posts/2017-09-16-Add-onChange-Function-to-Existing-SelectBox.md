---
title: "AWS EC2 User Data"
categories:
  - React
tags:
  - React
  - Javascript
  - Selectbox
---

{% include toc title="Add onChange function to an existing checkbox" icon="file-text" %}

## Introduction

If you can not change the file which renders the checkbox, you can use the following solution. 

## Solution

```liquid
document.getElementsByName('addressChange')[0].addEventListener(
                          'change',
                          function() {  alert('test'); },
                          false
                        );
```
