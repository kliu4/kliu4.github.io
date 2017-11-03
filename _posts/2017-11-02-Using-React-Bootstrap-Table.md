---
title: "Using React Bootstrap Table"
categories:
  - React
tags:
  - React
  - React Bootstrap Table
  - Twitter Bootstrap
---

{% include toc title="Using React Bootstrap Table" icon="file-text" %}

## Create React App and start

```
create-react-app mytable
npm start
```

## Install and Import React Bootstrap Table and Bootstrap

We need to install the Bootstrap as well. It is used to provide bootstrap css file.

```
npm install --save react-bootstrap-table
npm install bootstrap@4.0.0-beta.2
```

Add following lines at the begining of the App.js.

Note: we need to import css files as well.

```
import { BootstrapTable, TableHeaderColumn } from 'react-bootstrap-table';
import 'react-bootstrap-table/dist/react-bootstrap-table-all.min.css';
import 'bootstrap/dist/css/bootstrap.min.css';
```

## Test

Change the App.js to following to test

```
import React, { Component } from 'react';
import { BootstrapTable, TableHeaderColumn } from 'react-bootstrap-table';
import 'react-bootstrap-table/dist/react-bootstrap-table-all.min.css';
import 'bootstrap/dist/css/bootstrap.min.css';

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

class App extends Component {
  render() {
    return (
      <div className="App">
        <BootstrapTable data={products} version='4'>
          <TableHeaderColumn dataField="id" isKey={true} dataAlign="center" dataSort={true}>Product ID</TableHeaderColumn>
          <TableHeaderColumn dataField="name" dataSort={true}>Product Name</TableHeaderColumn>
          <TableHeaderColumn dataField="price" dataFormat={priceFormatter}>Product Price</TableHeaderColumn>
        </BootstrapTable>
      </div>
    );
  }
}

export default App;

```

