---
title: "React Project Not Recognize JSX file"
categories:
  - React
tags:
  - React
---

{% include toc title="React Project Not Recognize JSX file" icon="file-text" %}

## Description

I have a react project which doesn't recognize JSX file: when I import the component from JSX file, it says `cant not resove the file`; If I change `.jsx` extension to `.js`, then it works.

## Solution

Change the resove part in the `config/webpack.config.*.js`:

Then import the certificate using root:
```
    resolve: {
      modules: ['src', 'node_modules'],
      extensions: ['.js', '.json', '.jsx'],
      // Create aliases to import or require certain modules more easily
      alias: alias
    },
```
