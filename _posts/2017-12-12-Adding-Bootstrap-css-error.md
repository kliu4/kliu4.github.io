---
title: "You may need an appropriate loader to handle this file type with Webpack and CSS"
categories:
  - React
tags:
  - React
---

{% include toc title="You may need an appropriate loader to handle this file type with Webpack and CSS" icon="file-text" %}

## Problem

If you use `create-react-app`, you may not face this problem. 

If you use the old applicate framework, it may have this problem

{% raw %}
```liquid
ERROR in ./node_modules/bootstrap/dist/css/bootstrap.css
Module parse failed: node_modules/bootstrap/dist/css/bootstrap.css Unexpected token (7:5)
You may need an appropriate loader to handle this file type.
|  */
| /*! normalize.css v3.0.3 | MIT License | github.com/necolas/normalize.css */
| html {
|   font-family: sans-serif;
|   -webkit-text-size-adjust: 100%;
```
{% endraw %}


## Solution

Install following packages:

```liquid
npm install css-loader --save-dev
npm install style-loader --save-dev
npm install file-loader --save-dev
```

Add following rules in your `webpack.config.js`

```
rules: [
            {
                test: /\.css$/,
                use: [ 'style-loader', 'css-loader' ]
            },
            {
                test: /\.(woff|woff2|ttf|svg|eot)$/,
                use: [
                    {
                        loader: 'file-loader',
                        options: {}
                    }
                ]
            }]

```


