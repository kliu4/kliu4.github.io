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
    constructor(props) {
    super(props);
    this.onClick = this.onClick.bind(this);
  }
  
  onMapAction = (message) => {
    alert(message);
  }
  
  createCustomButtonGroup = props => {
    return (
      <ButtonGroup className='my-custom-class' sizeClass='btn-group-md'>
        { props.insertBtn }
        { props.deleteBtn }
        <button type='button'
          className={ `btn btn-primary` } onClick={() => this.onClick('Message')}>
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
