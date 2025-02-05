---
layout: default
title: "Dockerfile: Missing or \"latest\" version tag"
permalink: /infrastructure-security/missing-or-latest-version-tag
tags: ["plugin", "security"]
---

### Problem
Missing version tag or using the "latest" tag for the image.

### Description
When the version tag is missing, the latest version of the image will be used. Using the latest version can lead to unpredictable behavior when the image is updated.

**Examples:**
- You cannot know or control which version will be downloaded.
- If the image author is compromised and an attacker pushes a malicious Docker image, rebuilding your image could result in using the compromised version.
- Newer versions of Docker images could break the compatibility you depend on.

### Solution
Specify a version tag or digest value to ensure that the exact version of the Docker image is used.

### Problematic code
```dockerfile
ARG version=latest
FROM ubuntu as u1
FROM ubuntu:latest as u2
FROM ubuntu:$version as u3
```

### Verified code
```dockerfile
FROM ubuntu:noble as u1
FROM ubuntu@sha256:72297848456d5d37d1262630108ab308d3e9ec7ed1c3286a32fe09856619a782 as u2
```