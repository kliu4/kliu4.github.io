---
title: "No daemons for this host found - check host name in config.xml"
categories:
  - Computing
tags:
  - BOINC
  - Volunteer Computing
---

{% include toc title="No daemons for this host found - check host name in config.xml" icon="file-text" %}

## Introduction

Today I got an error when I tried to start the Boinc daemons:

```liquid
boincadm@climateathome:~/projects/climateathome$ bin/start 
Staying in ENABLED mode
Starting daemons
No daemons for this host found - check host name in config.xml
boincadm@climateathome:~/projects/climateathome$ bin/status 
BOINC is ENABLED

DAEMON  pid  status      lockfile disabled  commandline

TASK       last run       period          next run        lock file disabled  commandline
```

## Solution

My host is climateathome.info, and I have corrected set up the host name in my config.xml
```liquid
<master_url>https://climateathome.info/climateathome/</master_url>
<host>climateathome.info</host>
<db_name>climateathome</db_name>
```

But why does the error still exist?Then I found this link and got the following: the old version of BOINC uses first token of hostname to compare with the host in config.xml
```liquid
local_hostname = socket.gethostname()
local_hostname = local_hostname.split('.')[0]
```

Then I changed my config.xml to following and it works:
```liquid
<master_url>https://climateathome.info/climateathome/</master_url>
<host>climateathome</host>
<db_name>climateathome</db_name>
```
