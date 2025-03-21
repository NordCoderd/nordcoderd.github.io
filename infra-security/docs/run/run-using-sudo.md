---
layout: default
title: "Dockerfile: Avoid Using RUN with sudo"
permalink: /infrastructure-security/run-using-sudo
tags: ["plugin", "maintainability", "docker"]
---

### Problem
Using `RUN` with `sudo` commands leads to unpredictable behavior.

### Description
Docker executes `RUN` commands as the user specified by the `USER` directive, often root by default. Including `sudo` in `RUN` commands is redundant and may cause unexpected outcomes. Avoid using `sudo` to keep builds clean and predictable.

### Solution
Remove `sudo` from `RUN` commands. Use the appropriate `USER` directive to manage privileges.

### Problematic code
```dockerfile
FROM ubuntu:20.04
USER nobody
RUN sudo apt-get update && sudo apt-get install -y --no-install-recommends build-essential
```

### Verified code
```dockerfile
FROM ubuntu:20.04
USER nobody
RUN apt-get update && apt-get install -y --no-install-recommends build-essential
```