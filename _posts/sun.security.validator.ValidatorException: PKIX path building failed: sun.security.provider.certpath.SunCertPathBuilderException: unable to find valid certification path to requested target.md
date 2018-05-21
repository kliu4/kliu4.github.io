---
title: "sun.security.validator.ValidatorException: PKIX path building failed: sun.security.provider.certpath.SunCertPathBuilderException: unable to find valid certification path to requested target"
categories:
  - Java
tags:
  - SSL
---

{% include toc title="sun.security.validator.ValidatorException: PKIX path building failed: sun.security.provider.certpath.SunCertPathBuilderException: unable to find valid certification path to requested target
" icon="file-text" %}

## Description

I use mac and java to send get request to `geocode.arcgis.com` and getting following problem:

```
    sun.security.validator.ValidatorException: PKIX path building failed: sun.security.provider.certpath.SunCertPathBuilderException: unable to find valid certification path to requested target
```

## Solution

Download the certificate first:

```
openssl s_client -showcerts -connect geocode.arcgis.com:443 </dev/null 2>/dev/null|openssl x509 -outform PEM >mycertfile.pem
```


Then import the certificate using root:
```
keytool -import -alias example -keystore  $(/usr/libexec/java_home)/lib/security/cacerts -file ~/Downloads/InstallCert-master/mycertfile.pem 
```
