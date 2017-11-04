---
title: "Escape Double Curly Braces In Markdown"
categories:
  - Github
tags:
  - Github
  - Markdown
---

{% include toc title="Escape Double Curly Braces In Markdown" icon="file-text" %}

## Introduction

I have following code in markdown 

```
class ActiveFormatter extends React.Component {
  render() {
    return (
      <div style={{color: 'rgb(255,153,0)'}}>
        <FaCloudUpload size={32} />
      </div>
    );
  }
}
```

but it was rendered to following in the blog:

```
class ActiveFormatter extends React.Component {
  render() {
    return (
      <div style={{color: 'rgb(255,153,0)'}}>
        <FaCloudUpload size={32} />
      </div>
    );
  }
}
```


## solution

Wirte the code in following block:

 {% raw %}{%{% endraw %} raw %}
 {% raw %}{%{% endraw %} endraw %}
