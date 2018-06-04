---
title: "S3 CORS for Openlayers"
categories:
  - Computing
tags:
  - Cloud
---

{% include toc title="S3 CORS for Openlayers" icon="file-text" %}

## Introduction

Today I got following error when I add a KML layer from my bucket:

```
Failed to load https://s3.amazonaws.com/climateathomekml/KML_Samples.kml: No 'Access-Control-Allow-Origin' header is present on the requested resource. Origin 'http://localhost:3000' is therefore not allowed access.
```

## Solution

Set following CORS rules for `climateathomekml` bucket:

```
<?xml version="1.0" encoding="UTF-8"?>
<CORSConfiguration xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
<CORSRule>
    <AllowedOrigin>*</AllowedOrigin>
    <AllowedMethod>GET</AllowedMethod>
    <MaxAgeSeconds>3000</MaxAgeSeconds>
    <AllowedHeader>*</AllowedHeader>
</CORSRule>
</CORSConfiguration>
```
