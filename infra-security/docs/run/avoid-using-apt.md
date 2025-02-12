---
layout: default
title: "Dockerfile: Use apt-get or apt-cache Instead of apt"
permalink: /infrastructure-security/avoid-using-apt
tags: ["plugin", "maintainability", "docker"]
---

### Problem
Using `apt` in a Dockerfile can cause unpredictable behavior. apt is meant for end-user operations, not for scripting.

### Description
`apt` is designed for interactive use and may prompt for input, which is not suitable for automated Docker builds. Using `apt` may lead to errors or unexpected output. Instead, use `apt-get` or `apt-cache` for non-interactive package management.

### Solution
Replace `apt` with `apt-get` or `apt-cache` to ensure consistent, non-interactive execution in your Dockerfiles.

### Problematic code
```dockerfile
FROM ubuntu:20.04
USER nobody
RUN apt update && apt install -y build-essential
```

### Verified code
```dockerfile
FROM ubuntu:20.04
USER nobody
RUN apt-get update && apt-get install -y --no-install-recommends build-essential
```