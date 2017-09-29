---
title: "Always Run User Data when Launching Instance"
categories:
  - Computing
tags:
  - Cloud Computing
  - Amazon EC2
---

{% include toc title="Always Run User Data when Launching Instance" icon="file-text" %}

## Introduction

By default user data is executed once, at the first boot of the instance. Here is a similar question: https://aws.amazon.com/premiumsupport/knowledge-center/execute-user-data-ec2/

If you need to automatically restart the service but the instance has been configured. You could use  mime-multipart to append your new scripts to user data and set the cloud_final_modules as [scripts-user, always] to run the startup script everytime. You could set following as your user data and then start the instance:

## Solution
```liquid
Content-Type: multipart/mixed; boundary="//"
MIME-Version: 1.0

--//
Content-Type: text/cloud-config; charset="us-ascii"
MIME-Version: 1.0
Content-Transfer-Encoding: 7bit
Content-Disposition: attachment; filename="cloud-config.txt"

#cloud-config
cloud_final_modules:
- [scripts-user, always]

--//
Content-Type: text/x-shellscript; charset="us-ascii"
MIME-Version: 1.0
Content-Transfer-Encoding: 7bit
Content-Disposition: attachment; filename="userdata.txt"

#!/bin/bash
sudo service abc DEV start
--//
```
