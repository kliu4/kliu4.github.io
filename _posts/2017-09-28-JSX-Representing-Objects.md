---
title: "JSX Representing Objects"
categories:
  - React
tags:
  - React
  - Javascript
---

{% include toc title="JSX Representing Objects" icon="file-text" %}

## Introduction

JSX could be used to represent objects, following three representations are equal.

```liquid
const element = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);
```

```liquid
const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);
```

```
const element = {
  type: 'h1',
  props: {
    className: 'greeting',
    children: 'Hello, world'
  }
};
```

## Advanced

Following element has children and grandchildren. Followings are equal
```
<div className="commentBox">
    <h1>Comments</h1>
    <CommentList />
    <CommentForm />
</div>
```

```
React.createElement(
    "div",
    { className: "commentBox" },
    React.createElement(
        "h1",
        null,
        "Comments"
    ),
    React.createElement(CommentList, null),
    React.createElement(CommentForm, null)
);
```

## Tools
You could use Babel to convert them: https://babeljs.io/repl/
