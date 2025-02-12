---
layout: default
title: "Dockerfile: Clean Zypper Cache to Reduce Image Size"
permalink: /infrastructure-security/purge-zipper-cache
tags: ["plugin", "maintainability", "docker"]
---

### Problem
You do not run `zypper clean` after `zypper install`. This increases the layer and image size.

### Description
Cached package data from zypper can bloat your Docker image. Removing unneeded caches reduces the image size and improves build performance.

### Solution
Run `zypper clean` after installing packages with zypper. This command deletes cached package data and reduces the final image size.

### Problematic code
```dockerfile
FROM opensuse/leap:15.3
USER nobody
RUN zypper install -y httpd
```

### Verified code
```dockerfile
FROM opensuse/leap:15.3
USER nobody
RUN zypper install -y httpd && zypper clean
```