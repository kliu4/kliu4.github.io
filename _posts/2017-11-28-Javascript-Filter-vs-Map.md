---
title: "Javascript Filter vs Map"
categories:
  - React
tags:
  - React
  - Javascript
---

{% include toc title="Javascript Filter vs Map" icon="file-text" %}

## Introduction

Both the `filter()` and `map()` could use a callback to create a new array. However, they have some differents like following:

```
var newArray1 = arr.filter(callback);
var newArray2 = arr.map(callback);
```

## `filter()` vs `map()`

`filter()`'s callback is to test each element of the array. The callback return `true` or `false`. So, the `length of the new array does not have to be equal to the length of the old array`.

`map()`'s callback is to calculate an element for each element in the old array. Even if you add some condition to filter elements from old array, it still return new element (mostly it is `undefined`) for those old element do not meet the conditions. So, the `length of the new array has to be equal to the length of the old array`.

## Example

```
var a = [1, 2, 3, 4];
var b = a.filter(value => value !== 2);
var c = a.map(value => value * value);
var d = a.map(value => {
    if (value !== 2) {
       return value * value;
    }
});
```

The results are:
```
a = [1, 2, 3, 4]
b = [1, 3, 4]
c = [1, 4, 9, 16]
d = [1, undefined, 9, 16]
```
