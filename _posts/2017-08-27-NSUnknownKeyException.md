---
title: "NSUnknownKeyException"
categories:
  - Swift
tags:
  - Swift
---

{% include toc title="NSUnknownKeyException" icon="file-text" %}

## Introduction

Today I followed the online tutorial to write the foodtruck application. I control+dragged the Lable to ViewController but then I found I didn't change the button to action. Then I removed the line like this " @IBOutlet weak var setDefaultLableText: UIButtonl!". Then I got the following error:

```liquid
2017-09-10 23:35:50.154 Foodtruck[4796:2553036] *** Terminating app due to uncaught exception 'NSUnknownKeyException', reason: '[<Foodtruck.ViewController 0x7fac0c6062b0> setValue:forUndefinedKey:]: this class is not key value coding-compliant for the key setefaultLableText.'
```

## Solution

It is because: although code was deleted, it still needs to delete from the connect.  

*Colick the right part, there is an arraw (connection inspector)  
*Delete the wrong connection  
*Then it should work  
