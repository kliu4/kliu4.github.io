---
title: "Customize the Input for React-S3-Uploader"
categories:
  - React
tags:
  - React
---

{% include toc title="Customize the Input for React-S3-Uploader" icon="file-text" %}

## Problem

The default file input of React-S3-Uploader is very ugly, we could use `bootstrap` to customize it. Following is to customize it and add a progressbar

## Solution

<a href="/assets/images/image-filename-2-large.jpg"><img src="/assets/images/customize-react-s3-uploader.png"></a>

{% raw %}
```liquid
<div className="input-group">
                    <label className="input-group-btn">
                    <span className="btn btn-primary">
                        <Glyphicon glyph="paperclip" />Browse
                        <ReactS3Uploader style={{display: 'none'}}
                                         signingUrl="s3/sign"
                                         signingUrlMethod="GET"
                                         preprocess={this.onUploadStart}
                                         onProgress={this.onUploadProgress}
                                         onFinish={this.onUploadFinish}
                                         signingUrlHeaders={getAuthHeader()}
                                         uploadRequestHeaders={{'x-amz-acl': 'public-read'}}
                                         contentDisposition="attachment"
                                         scrubFilename={(filename) => filename.replace(/[^\w\d_\-.]+/ig, '')}
                                         server={`${fieldComplianceApiUrl}`}/>
                    </span>
                    </label>
                    <FormControl readOnly value={this.state.file}/>
                </div>
                <br/>
                <div>
                    <ProgressBar striped bsStyle="success" now={this.state.completed}
                                 label={`${this.state.completed}%`}/>
                </div>
```
{% endraw %}
