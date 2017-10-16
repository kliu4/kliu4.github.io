---
title: "Spring Boot Thymeleaf Parsing Document Exception"
categories:
  - Java
tags:
  - Spring boot
  - Thymeleaf
  - HTML5
  - Twitter Bootstrap
---

{% include toc title="Spring Boot Thymeleaf Parsing Document Exception" icon="file-text" %}

## Introduction

Today I use Spring boot initializer creating a project with `web`, `security` and `thymeleaf` tags. The I place the `bootstrap adminLTE` in the project. After login, I go the following error:

```liquid
Whitelabel Error Page

This application has no explicit mapping for /error, so you are seeing this as a fallback.

Mon Oct 16 18:48:17 CDT 2017
There was an unexpected error (type=Internal Server Error, status=500).
Exception parsing document: template="dashboard/index", line 35 - column 3
```

## Solution

In application.properties, add the following lines

```liquid
# ThymeLeaf
spring.thymeleaf.mode=LEGACYHTML5
spring.thymeleaf.cache=false
```

In pom.xml, add the following dependency

```liquid
<dependency>
			<groupId>net.sourceforge.nekohtml</groupId>
			<artifactId>nekohtml</artifactId>
			<version>1.9.22</version>
</dependency>
```

