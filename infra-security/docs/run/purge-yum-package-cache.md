---
layout: default
title: "Dockerfile: Clean YUM Package Cache to Reduce Image Size"
permalink: /infrastructure-security/purge-yum-package-cache
tags: ["plugin", "maintainability", "docker"]
---

### Problem
You do not run `yum clean all` after `yum install`. This increases the image size.

### Description
Cached package data bloats the image if not removed. Cleaning the yum cache reduces image size and improves performance.

### Solution
Run `yum clean all` after `yum install` to clear cached data and reduce image size.

### Problematic code
```dockerfile
FROM centos:7
USER nobody
RUN yum install -y httpd
```

### Verified code
```dockerfile
FROM centos:7
USER nobody
RUN yum install -y httpd && yum clean all
```