---
layout: default
title: "Dockerfile: Use WORKDIR Instead of 'RUN cd ...'"
permalink: /infrastructure-security/use-workdir-over-cd
tags: ["plugin", "maintainability", "docker"]
---

### Problem
Using `RUN cd ...` to change directories makes the Dockerfile hard to read and maintain.

### Description
Using multiple `RUN cd ... && ...` instructions creates clutter. These commands are difficult to troubleshoot and maintain. Instead, use the `WORKDIR` instruction to set the working directory consistently. This approach simplifies the Dockerfile and improves readability.

### Solution
Replace `RUN cd ...` commands with a `WORKDIR` instruction. This method provides a clear and persistent working directory for subsequent commands.

### Problematic code
```dockerfile
FROM ubuntu:20.04
USER nobody
RUN cd /app && make build
```

### Verified code
```dockerfile
FROM ubuntu:20.04
USER nobody
WORKDIR /app
RUN make build
```