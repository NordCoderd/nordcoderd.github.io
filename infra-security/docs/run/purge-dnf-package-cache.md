---
layout: default
title: "Dockerfile: Clean DNF Package Cache to Reduce Image Size"
permalink: /infrastructure-security/purge-dnf-package-cache
tags: ["plugin", "maintainability", "docker"]
---

### Problem
The Dockerfile is missing the `dnf clean all` command. Cached package data increases the image size.

### Description
Cached package data from DNF can bloat the image if not removed. Cleaning the cache ensures a leaner image and better maintainability.

### Solution
Add `dnf clean all` after installing packages to remove cached data and reduce the image size.

### Problematic code
```dockerfile
FROM fedora:version
USER nobody
RUN dnf install -y httpd
```

### Verified code
```dockerfile
FROM fedora:version
USER nobody
RUN dnf install -y httpd && dnf clean all
```