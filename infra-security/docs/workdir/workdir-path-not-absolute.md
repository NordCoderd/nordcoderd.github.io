---
layout: default
title: "Dockerfile: Use Absolute Paths for WORKDIR"
permalink: /infrastructure-security/workdir-path-not-absolute
tags: ["plugin", "maintainability", "docker"]
---

### Problem
The `WORKDIR` path is not absolute. This can lead to confusion and errors.

### Description
For clarity and reliability, you should always use absolute paths for your `WORKDIR`. Relative paths may cause unexpected behavior during builds.

### Solution
Specify an absolute path in the `WORKDIR` instruction to ensure consistent behavior.

### Problematic code
```dockerfile
FROM ubuntu:20.04
USER nobody
WORKDIR app
```

### Verified code
```dockerfile
FROM ubuntu:20.04
USER nobody
WORKDIR /app
```