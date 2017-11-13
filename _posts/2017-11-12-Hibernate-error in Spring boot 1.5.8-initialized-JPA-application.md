---
title: "Hibernate error in Spring boot 1.5.8 initialized JPA application"
categories:
  - Java
tags:
  - Spring
  - Spring Boot
  - JPA
  - Maven
---

{% include toc title="Hibernate error in Spring boot 1.5.8 initialized JPA application" icon="file-text" %}

## Introduction

I use spring boot to initialize a web application with JPA, however, it doesn't allow me to start the application. It shows the hibernate error. It is supposed the spring-boot-starter-data-jpa will install related dependencies but it seems not:

```liquid
Caused by: java.lang.ClassNotFoundException: org.hibernate.HibernateException
    at java.net.URLClassLoader.findClass(URLClassLoader.java:381) ~[na:1.8.0_144]
    at java.lang.ClassLoader.loadClass(ClassLoader.java:424) ~[na:1.8.0_144]
    at sun.misc.Launcher$AppClassLoader.loadClass(Launcher.java:335) ~[na:1.8.0_144]
    at java.lang.ClassLoader.loadClass(ClassLoader.java:357) ~[na:1.8.0_144]
    ... 60 common frames omitted
```

## Solution

Don't need to add the hibernate dependency, just change the Spring Boot Version to latest version

```
 <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>1.5.8</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
```

