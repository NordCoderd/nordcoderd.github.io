---
layout: default
title: "Dockerfile Security: Avoid Overriding ARG Variables in RUN Commands"
permalink: /infrastructure-security/arg-variables-overridden
tags: ["plugin", "security", "docker"]
---

### Problem
Using `ARG` variables in `RUN` commands can be overridden by users. This leads to unintended behaviors and security risks.

### Description
ARG variables are set at build time. Users can override them with the `--build-arg` flag. Critical commands may change if the `ARG` is altered. This behavior can introduce security risks or unexpected outcomes.

### Solution
Avoid using `ARG` variables directly in `RUN` commands for critical operations. Use fixed values or other secure methods to ensure consistent behavior.

### Problematic code
```dockerfile
FROM ubuntu:20.04
USER nobody
ARG INSTALL_PACKAGE=build-essential
RUN apt-get update && apt-get install -y $INSTALL_PACKAGE
```

### Verified code
```dockerfile
FROM ubuntu:20.04
USER nobody
RUN apt-get update && apt-get install --no-install-recommends -y build-essential
```