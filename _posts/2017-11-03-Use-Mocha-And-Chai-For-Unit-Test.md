---
title: "Use Mocha and Chai for Unit Test"
categories:
  - React
tags:
  - React
  - Unit Test
  - NodeJS
  - Mocha
  - Chai
---

{% include toc title="Use Mocha and Chai for Unit Test" icon="file-text" %}

## Install Mocah and Chai

```liquid
npm install mocha --save
npm install chai --save
```

## Test Fucntions

app.js

{% raw %}
```liquid
module.exports = {
  sayHello: function(){
    return 'hello';
  },
  addNumbers: function(val1, val2){
    return val1 + val2;
  }
}
```
{% endraw %}

appTest.js

{% raw %}
```liquid
const assert = require('chai').assert;
const app = require('../app');

sayHelloResult = app.sayHello();
addNumbersResult = app.addNumbers(5, 5);

describe('App', function(){
  describe('sayHello', function(){
    it('sayHello should return hello', function(){
      assert.equal(sayHelloResult, 'hello');
    });

    it('sayHello should return string', function(){
      assert.typeOf(sayHelloResult, 'string');
    });
  });

  describe('addNumbers', function(){
    it('addNumbers should be above 5', function(){
      assert.isAbove(addNumbersResult, 5);
    });

    it('addNumbers should return type number', function(){
      assert.typeOf(addNumbersResult, 'number');
    });
  });
});
```
{% endraw %}

