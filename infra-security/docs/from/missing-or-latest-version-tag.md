---
layout: default
title: "Dockerfile Security: Avoid Missing or 'latest' Version Tags"
permalink: /infrastructure-security/missing-or-latest-version-tag
tags: ["plugin", "security", "docker"]
---

### Problem
Docker images without a version tag or with the "latest" tag use unpredictable versions.

### Description
When you do not specify a version tag, Docker uses the latest version by default. This practice makes builds unpredictable. You do not know which image version you will download. If an attacker compromises the image author, they can push a harmful image. New image updates may also break your application.

### Examples
- The image version is not controlled.
- An attacker can push a malicious image as the latest tag.
- Updates may break your application due to incompatibility.

### Solution
Always specify a version tag or digest. This practice ensures that you use a fixed and known image version.

### Problematic code
```dockerfile
ARG version=latest
FROM ubuntu as u1
FROM ubuntu:latest as u2
FROM ubuntu:$version as u3
FROM u3
```

### Verified code
```dockerfile
FROM ubuntu:noble as u1
FROM ubuntu@sha256:72297848456d5d37d1262630108ab308d3e9ec7ed1c3286a32fe09856619a782 as u2
FROM u2
```