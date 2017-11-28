---
title: "Add Customized Buttons in React Bootstrap Table"
categories:
  - React
tags:
  - React
  - React Bootstrap Table
---

{% include toc title="Use React Modal in React Bootstrap Table" icon="file-text" %}

## Solution

It is easy if you don't need to customize the insert modal and delete modal, just follow http://allenfang.github.io/react-bootstrap-table/example.html#custom

If you have customized the insert modal and delete modal, do it like followigns:

{% raw %}
```liquid
class UploadFormatter extends React.Component {
  createCustomButtonGroup = props => {
    return (
      <ButtonGroup className='my-custom-class' sizeClass='btn-group-md'>
        { props.insertBtn }
        { props.deleteBtn }
        <button type='button'
          className={ `btn btn-primary` }>
          MyCustomBtn
        </button>
      </ButtonGroup>
    );
  }

  render() {
    const selectRow = {
      mode: 'checkbox'
    };
    const options = {
      insertModalHeader: this.createCustomModalHeader,
      insertModalFooter: this.createCustomModalFooter,
      insertModalBody: this.createCustomModalBody,
      insertText: 'Upload',
      afterDeleteRow: this.onAfterDeleteRow,
      btnGroup: this.createCustomButtonGroup
    };
    return (
      <BootstrapTable data={ products }
        options={ options }
        selectRow={ selectRow }
        insertRow
        deleteRow
        exportCSV>
        <TableHeaderColumn dataField='id' isKey={ true }>Product ID</TableHeaderColumn>
        <TableHeaderColumn dataField='name'>Product Name</TableHeaderColumn>
        <TableHeaderColumn dataField='price'>Product Price</TableHeaderColumn>
      </BootstrapTable>
    );
  }
}
```
{% endraw %}

## Final File

{% raw %}
```liquid
import React, { Component } from 'react';
import { BootstrapTable, TableHeaderColumn } from 'react-bootstrap-table';
import 'react-bootstrap-table/dist/react-bootstrap-table-all.min.css';
import 'bootstrap/dist/css/bootstrap.min.css';
import FaCloudUpload from 'react-icons/lib/fa/cloud-upload';
import Modal from 'react-modal';

// products will be presented by react-bootstrap-table
var products = [{
      id: 1,
      name: "Item name 1",
      price: 100
  },{
      id: 2,
      name: "Item name 2",
      price: 100
  },{
      id: 3,
      name: "Item name 3",
      price: 100
  },{
      id: 4,
      name: "Item name 4",
      price: 100
  },{
      id: 5,
      name: "Item name 5",
      price: 100
  }];

// It's a data format example.
function priceFormatter(cell, row){
  return '<i class="glyphicon glyphicon-usd"></i> ' + cell;
}

const customStyles = {
  content : {
    top                   : '50%',
    left                  : '50%',
    right                 : 'auto',
    bottom                : 'auto',
    marginRight           : '-50%',
    transform             : 'translate(-50%, -50%)'
  }
};

class UploadFormatter extends React.Component {
  constructor() {
    super();

    this.state = {
      modalIsOpen: false
    };

    this.openModal = this.openModal.bind(this);
    this.afterOpenModal = this.afterOpenModal.bind(this);
    this.closeModal = this.closeModal.bind(this);
  }

  openModal() {
    this.setState({modalIsOpen: true});
  }

  afterOpenModal() {
    // references are now sync'd and can be accessed.
    this.subtitle.style.color = '#f00';
  }

  closeModal() {
    this.setState({modalIsOpen: false});
  }

  render() {
    return (
      <div>
        <div style={{color: 'rgb(255,153,0)'}}>
            <FaCloudUpload size={32} onClick={this.openModal} />
        </div>
        <Modal
          isOpen={this.state.modalIsOpen}
          onAfterOpen={this.afterOpenModal}
          onRequestClose={this.closeModal}
          style={customStyles}
          contentLabel="Example Modal"
        >

          <h2 ref={subtitle => this.subtitle = subtitle}>Hello</h2>
          <button onClick={this.closeModal}>close</button>
          <div>I am a modal</div>
          <form>
            <input />
            <button>tab navigation</button>
            <button>stays</button>
            <button>inside</button>
            <button>the modal</button>
          </form>
        </Modal>
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
{% endraw %}
