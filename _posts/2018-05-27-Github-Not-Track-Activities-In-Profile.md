---
title: "Github not track activities in profile"
categories:
  - Others
tags:
  - Github
---

{% include toc title="Github not track activities in profile" icon="file-text" %}

## Introduction

I created a new repository in Github, then used following command lines to commit my changes, but my Github profile page doesn't tract my activites.

```liquid
git add .
git commit -m "first commit"
git remote add origin https://github.com/kliu4/climateathome.git
git push -u origin master
```

## Solution

This is because I used `https` as my remote url, if change to `ssh` url then everything will be OK.

Step 1: using following command to create a ssh key pair:

```
ssh-keygen
```

When run this command, just hit `enter` to select default parameters. It will create keypair named `id_rsa` under `~/.ssh`.

Step 2: copy contents from `~/.ssh/id_rsa.pub`

Step 3: following github page (https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/) to paste your key contents in step 2 ass ssh key

Step 4: clone your project using the `ssh` link which could be find via click `clone or download` of your project, then commit and push


```
git clone git@github.com:kliu4/climateathome.git
cd climateathome
git add .
git commit -m "first commit"
git push -u origin master
```
