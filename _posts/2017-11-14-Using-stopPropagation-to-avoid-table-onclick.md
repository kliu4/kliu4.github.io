---
title: "Using stopPropagation to avoid table onclick"
categories:
  - React
tags:
  - React
  - React Bootstrap Table
  - Mocha
  - Chai
  - Enzyme
---

{% include toc title="Using stopPropagation to avoid table onclick" icon="file-text" %}

## Introduction

The table has is own onclick function, e.g, click one cell to select the row. Then if there is a button or icon in the cell, the button's `onclick` conflicts tables `onclick` function.

## Solution

In button or icon's `onlick` fucntion, add `e.stopPropagation();`

e.g.,

Following is my icon in `react-s3-table`:

## Pseudocode

{% raw %}
```liquid
<div style={{color: 'rgb(255,153,0)'}}>
      <FaCloudUpload size={32} onClick={this.openModal}/>
</div>
```
{% endraw %}

Then change the `openModal(e)` function to following:

```liquid
openModal(e) {
    e.stopPropagation();
    this.setState({modalIsOpen: true});
}
```

## Using `Enzyme` to test the `onclick`:

{% raw %}
```liquid
describe('AttachmentModal', () => {
  const minProps = {
    id: "",
    row: {}
  };

  it('should render without exploding', () => {
    const wrapper = shallow(<AttachmentModal {...minProps}/>);
    expect(wrapper.length).to.equal(1);
  });

  it('should open modal when button is clicked', () => {
    const wrapper = shallow(<AttachmentModal {...minProps}/>);
    wrapper.find(FaCloudUpload).simulate('click', { stopPropagation: () => undefined });
    expect(wrapper.find(Modal).prop('modalIsOpen')).to.equal(true);
  });
});
```
{% endraw %}


