---
title: "npm install Not Install changes of package.json"
categories:
  - React
tags:
  - React
---

{% include toc title="npm install Not Install changes of package.json" icon="file-text" %}

## Introduction

I have added some modules in `package.json`, but when I run the `npm install`, it doesn't install added modules.

## Solution

Delete the `package-lock.json`, then run the `npm install` again

```
kliu$ npm install
up to date in 6.376s
kliu$ rm -rf package-lock.json
kliu$ npm install
npm notice created a lockfile as package-lock.json. You should commit this file.
added 26 packages in 9.651s
```

