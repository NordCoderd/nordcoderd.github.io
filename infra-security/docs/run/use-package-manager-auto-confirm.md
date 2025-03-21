---
layout: default
title: "Dockerfile: Use Package Manager Auto-Confirm Flag '-y'"
permalink: /infrastructure-security/use-package-manager-auto-confirm
tags: ["plugin", "maintainability", "docker"]
---

### Problem
Package manager calls lack the `-y` flag. This may require manual input.

### Description
Package managers like `apt-get`, `yum`, `dnf`, and `zypper` prompt for confirmation if the `-y` flag is missing. Without this flag, installations may pause for manual input and block automated builds.
### Solution
Always add the `-y` flag to package manager commands. This guarantees auto-confirmation and supports fully automated builds.

### Problematic code
```dockerfile
FROM ubuntu:20.04
USER nobody
RUN apt-get update && apt-get install --no-install-recommends build-essential
```

### Verified code
```dockerfile
FROM ubuntu:20.04
USER nobody
RUN apt-get update && apt-get install -y --no-install-recommends build-essential
```