---
layout: default
title: "Dockerfile: Standardise Remote GET Tools"
permalink: /infrastructure-security/standardise-remote-get
tags: ["plugin", "maintainability", "docker"]
---

### Problem
Using both `wget` and `curl` in RUN commands is redundant and complicates maintenance.

### Description
Both `wget` and `curl` fetch remote files. Using both tools adds unnecessary redundancy and may lead to installing extra packages. Standardise on one tool to keep the Dockerfile clear and efficient.

### Solution
Choose one tool, either `wget` or `curl`, and use it consistently in your Dockerfile.

### Problematic code
```dockerfile
FROM ubuntu:20.04
USER nobody
RUN wget http://example.com/script.sh -O script.sh && curl -sSL http://example.com/script.sh -o script2.sh
```

### Verified code
```dockerfile
FROM ubuntu:20.04
USER nobody
RUN curl -sSL http://example.com/script.sh -o script.sh
```