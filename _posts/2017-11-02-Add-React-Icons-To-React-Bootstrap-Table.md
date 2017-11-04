---
title: "Add React Icons to React Bootstrap Table"
categories:
  - React
tags:
  - React
  - React Icons
  - React Bootstrap Table
---

{% include toc title="Add React Icons to React Bootstrap Table" icon="file-text" %}

## Install React Icons

```
npm install react-icons --save
```

## Import Icons 

Note, the react icons website has error. The icons should be imported like following:

```
import FaCloudUpload from 'react-icons/lib/fa/cloud-upload';
```


## Render Icons in Component

Following is to create icon with size 32 and color (Amazon Orange)

{% raw %}
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

function uploadFormatter(cell, row) {
  return (
    <UploadFormatter active={ cell } />
  );
}
```
{% endraw %}

## Final File

```liquid
import React, { Component } from 'react';
import { BootstrapTable, TableHeaderColumn } from 'react-bootstrap-table';
import 'react-bootstrap-table/dist/react-bootstrap-table-all.min.css';
import 'bootstrap/dist/css/bootstrap.min.css';
import FaCloudUpload from 'react-icons/lib/fa/cloud-upload';

// products will be presented by react-bootstrap-table
var products = [{
      id: 1,
      name: "Item name 1",
      price: 100
  },{
      id: 2,
      name: "Item name 2",
      price: 100
  }];
// It's a data format example.
function priceFormatter(cell, row){
  return '<i class="glyphicon glyphicon-usd"></i> ' + cell;
}


class UploadFormatter extends React.Component {
  render() {
    return (
      <div style= { {color: 'rgb(255,153,0)'} }>
        <FaCloudUpload size={32} />
      </div>
    );
  }
}

function uploadFormatter(cell, row) {
  return (
    <UploadFormatter active={ cell } />
  );
}

class App extends Component {
  render() {
    return (
      <div className="App">
        <BootstrapTable data={products} version='4'>
          <TableHeaderColumn dataField="id" isKey={true} dataAlign="center" dataSort={true}>Product ID</TableHeaderColumn>
          <TableHeaderColumn dataField="name" dataSort={true}>Product Name</TableHeaderColumn>
          <TableHeaderColumn dataField="price" dataFormat={priceFormatter}>Product Price</TableHeaderColumn>
          <TableHeaderColumn dataField="checked" dataFormat={uploadFormatter}>Product Upload</TableHeaderColumn>
        </BootstrapTable>
      </div>
    );
  }
}

export default App;

```
