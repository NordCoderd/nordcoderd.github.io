---
layout: default
title: "Dockerfile: Use --no-install-recommends with apt-get"
permalink: /infrastructure-security/no-install-recommends
tags: ["plugin", "maintainability", "docker"]
---

### Problem
Not using `--no-install-recommends` with `apt-get` installs unnecessary packages and bloats the image.

### Description
When you run `apt-get` install without `--no-install-recommends`, Docker installs extra packages by default. This increases the image size and may add unwanted dependencies. Using `--no-install-recommends` installs only the essential packages, reducing the image size and potential security risks.

### Solution
Always add the `--no-install-recommends` flag when installing packages with `apt-get` to ensure only required packages are installed.

### Problematic code
```dockerfile
FROM ubuntu:20.04
USER nobody
RUN apt-get update && apt-get install -y build-essential
```

### Verified code
```dockerfile
FROM ubuntu:20.04
USER nobody
RUN apt-get update && apt-get install --no-install-recommends -y build-essential
```