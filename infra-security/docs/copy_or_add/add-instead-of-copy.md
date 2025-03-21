---
layout: default
title: "Dockerfile: Use COPY Instead of ADD Unless Extracting Tar Files"
permalink: /infrastructure-security/add-instead-of-copy
tags: ["plugin", "maintainability", "docker"]
---

### Problem
Using `ADD` instead of `COPY` can lead to unexpected behavior.

### Description
`ADD` has extra features, such as extracting tar files and handling remote URLs. These features may cause unintended effects if you only need to copy files. Use `COPY` to ensure simple and predictable behavior.

### Solution
Replace `ADD` with `COPY` unless you need the extra functionality provided by ADD.

### Problematic code
```dockerfile
FROM ubuntu:20.04
USER nobody
ADD ./app /app
```

### Verified code
```dockerfile
FROM ubuntu:20.04
USER nobody
COPY ./app /app
```