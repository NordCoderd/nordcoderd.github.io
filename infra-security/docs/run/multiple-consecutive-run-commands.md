---
layout: default
title: "Dockerfile: Consolidate Multiple RUN Instructions"
permalink: /infrastructure-security/multiple-consecutive-run-commands
tags: ["plugin", "maintainability", "docker"]
---

### Problem
Multiple consecutive `RUN` instructions create extra layers and make the Dockerfile harder to maintain.

### Description
Each `RUN` instruction creates a new image layer, which increases the final image size and build time. Consolidating these commands into a single `RUN` instruction improves efficiency and simplifies maintenance.

### Solution
Combine consecutive `RUN` commands using `&&` to reduce the number of layers.

### Problematic code
```dockerfile
FROM ubuntu:20.04
RUN apt-get -y --no-install-recommends install netcat
RUN apt-get clean
USER nobody
```

### Verified code
```dockerfile
FROM ubuntu:20.04
RUN apt-get -y --no-install-recommends install netcat && apt-get clean
USER nobody
```