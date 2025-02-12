---
layout: default
title: "Dockerfile: Avoid Deprecated MAINTAINER Instruction"
permalink: /infrastructure-security/deprecated-maintainer-used
tags: ["plugin", "maintainability", "docker"]
---

### Problem
The Dockerfile uses a deprecated `MAINTAINER` instruction. This instruction is no longer recommended.

### Description
`MAINTAINER` has been deprecated since Docker 1.13.0. Use LABEL to provide maintainer information. This change improves clarity and maintainability.

### Solution
Remove the `MAINTAINER` instruction from your Dockerfile. Use LABEL to specify maintainer details.

### Problematic code
```dockerfile
FROM ubuntu:20.04
USER nobody
MAINTAINER John Doe <john.doe@example.com>
```

### Verified code
```dockerfile
FROM ubuntu:20.04
USER nobody
LABEL org.opencontainers.image.authors="John Doe <john.doe@example.com>"
```