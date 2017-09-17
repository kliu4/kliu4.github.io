---
title: "AWS EC2 User Data"
categories:
  - Cloud
tags:
  - AWS
  - EC2
  - Cloud-init
---

{% include toc title="AWS EC2 User Data" icon="file-text" %}

## Introduction

User Data is the shell script file or cloud-init commands which could be passed to Cloud Instance. The Cloud exceutes the User Data **at the first launch**. 

## Create the User Data when launch the instance

It is easy and straightforward to create the User Data when launch the instance, following is one exmaple

```liquid
#!/bin/bash
touch /tmp/testfile
```

In this example, the first line is mandatory. Each User Data with shell scripts should be started with the line ```#!/bin/bash```

## Append User Data after launch

Sometimes after instance launch, we still want to append some shell scripts. So AWS provides the fucntion to change the User Data:  
*Stop the instance  
*Click View/Change User Data to edit the User Data  
*Start the instance  

However, you need user `multipart` to append the file. Following is the example from AWS website  
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
/bin/echo "Hello World." >> /tmp/sdksdfjsdlf
--//
```

For the above example, you could replace the lines under `#!/bin/bash` but you need keep all the lines above it. This is because:

*It uses mime-multipart to append the User Data  
*It uses `[scripts-user, always]` to run the User Data  

## Cloud-init log path

*/var/lib/cloud/instance/scripts/, e.g., part-001  
*/var/log/cloud-init.log  
*/var/log/cloud-init-output.log  

