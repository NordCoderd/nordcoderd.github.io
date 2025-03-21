---
layout: default
title: "Dockerfile: Avoid Using 'dist-upgrade' in Package Management"
permalink: /infrastructure-security/no-dist-upgrade
tags: ["plugin", "maintainability", "docker"]
---

### Problem
The package manager `dist-upgrade` upgrades a major version and is not suitable for Dockerfiles.

### Description
Using `dist-upgrade` can upgrade to a new major release. This behavior may break your Dockerfile by introducing unexpected changes. Dockerfiles should use controlled updates to maintain stability.

### Solution
Just use newer version of a Docker image.

### Problematic code
```dockerfile
FROM ubuntu:20.04
USER nobody
RUN apt-get dist-upgrade
```

### Verified code
```dockerfile
# just use newer version of image
```