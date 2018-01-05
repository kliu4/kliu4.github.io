---
title: "Java Design Patterns"
categories:
  - Java
tags:
  - Java
---

{% include toc title="Java Design Patterns" icon="file-text" %}

## Introduction

`Design Patterns` are general architectural solutions. Following `Design Patterns` could speed up the development of robust applications.

## SOLID Design Principles

### Single Responsibility Principle (SSR)

A Class will do one thing only.

### Open-Closed Principle (OCP)

Class should be open to extension, but closed for modification.

### Liskov Substitution Principle (LSP)

Any places use the parent class could be replaced by subtype class without errors.

### Interface Segregation Principle (ISP)

Segregate interfaces to small interfaces rather than using one big interface. 

### Dependency Inversion Principle (DIP)

A. High-level module should not depend on Low-level modules, both should depend on abstractions  
B. Abstractions should not depend on details, details should depend on abstractions

High Level Classes --> Abstraction Layer --> Low Level Classes

