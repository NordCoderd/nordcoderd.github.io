---
layout: default
title: "Dockerfile: Combine Package Manager Update and Install in a Single RUN Instruction"
permalink: /infrastructure-security/update-and-install-single-run
tags: ["plugin", "maintainability", "docker"]
---

### Problem
Using `RUN <package-manager> update` alone is risky. It should be followed by `<package-manager> install` in the same RUN command.

### Description
Running the package manager update command alone updates the package list in a separate layer. This updated list may not be used if the installation occurs in another RUN statement. Combining the update and install commands in one RUN ensures that the package installation uses the latest package data. 

Supported package managers include: `apt-get`, `apt`, `yum`, `apk`, `dnf`, and `zypper`.

### Solution
Combine `<package-manager> update` and `<package-manager> install` in one RUN command. This approach guarantees that the updated package list is applied immediately during installation.

### Problematic code
```dockerfile
FROM ubuntu:20.04
USER nobody
RUN apt-get update
RUN apt-get install -y --no-install-recommends build-essential
```

### Verified code
```dockerfile
FROM ubuntu:20.04
USER nobody
RUN apt-get update && apt-get install --no-install-recommends -y build-essential
```