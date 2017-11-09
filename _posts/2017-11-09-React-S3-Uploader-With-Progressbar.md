---
title: "React S3 Uploader with Progressbar"
categories:
  - React
tags:
  - React
  - React S3 Uploader
  - React Bootstrap 
---

{% include toc title="React S3 Uploader with Progressbar" icon="file-text" %}

## Introduction and Installation

React-S3-Uploader provides convinent way to upload files from browser rather than from server

### Installation in Client-Side Application
```liquid
npm install --save react-s3-uploader
npm install --save react-bootstrap
```

### Installation in Server-Side Application
```liquid
npm install --save react-s3-uploader
npm install --save aws-config
npm install --save bluebird
```

## Render the Uploader and ProgressBar

I render the Uploader and ProgressBar in React Modal

{% raw %}
```liquid
import {ProgressBar} from 'react-bootstrap';
const ReactS3Uploader = require('react-s3-uploader');

class AttachmentBody extends React.Component {
  constructor(props) {
    super(props);
    this.onUploadFinish = this.onUploadFinish.bind(this);
    this.onUploadProgress = this.onUploadProgress.bind(this);
    this.state = {completed: 0};
  }

  onUploadProgress(percent){
    this.setState({completed: percent});
  }

  onUploadFinish( e ){
    //Do things here
  }

  render() {
    return (
      <div className='modal-body'>
        <ReactS3Uploader
          signingUrl="s3/sign"
          signingUrlMethod="GET"
          onProgress={this.onUploadProgress}
          onFinish={this.onUploadFinish}
          signingUrlHeaders={getAuthHeader()}
          uploadRequestHeaders={{ 'x-amz-acl': 'public-read' }}
          contentDisposition="auto"
          scrubFilename={(filename) => filename.replace(/[^\w\d_\-.]+/ig, '')}
          server="http://localhost:3001" />
        <br />
        <div>
          <ProgressBar striped bsStyle="success" now={this.state.completed}  label={`${this.state.completed}%`}/>
        </div>
      </div>
    );
  }
}
```
{% endraw %}

## Using Server Side to Provide Signature Method

### Method1: Using Router

`getFileKeyDir` could be used to add prefix to the s3 location, e.g., you could upload to s3Bucket/aa/bb/cc/UUID_yourfile.txt

{% raw %}
```liquid
router.use(`/s3`, require('react-s3-uploader/s3router')({
    bucket: s3Bucket,
    headers: {'Access-Control-Allow-Origin': '*', 'Access-Control-Allow-Headers': 'Origin, X-Requested-With, Content-Type, Accept'},
    getFileKeyDir: function(req) {
        return s3Prefix;
    },
    ACL: 'private',
    uniquePrefix: true
}));
```
{% endraw %}

### Method2: Using App

{% raw %}
```liquid
app.use(`/s3`, require('react-s3-uploader/s3router')({
    bucket: s3Bucket,
    headers: {'Access-Control-Allow-Origin': '*', 'Access-Control-Allow-Headers': 'Origin, X-Requested-With, Content-Type, Accept'},
    getFileKeyDir: function(req) {
        return s3Prefix;
    },
    ACL: 'private',
    uniquePrefix: true
}));
```
{% endraw %}
