---
layout: default
title: "Dockerfile: Use '-l' Flag with useradd to Prevent High UID Issues"
permalink: /infrastructure-security/useradd-missing-l-flag-high-uid
tags: ["plugin", "maintainability", "docker"]
---

### Problem
Using `useradd` without the `-l` flag can assign a high UID, which may lead to an excessively large image.

### Description
When you create a user without the `-l` flag, the system may assign a high UID by default. High UIDs can result in additional metadata and unforeseen side effects that bloat the image size.

### Solution
Always add the `-l` flag with `useradd` to assign a lower UID. This practice avoids unnecessary image bloat and potential permission issues.

### Problematic code
```dockerfile
FROM ubuntu:20.04
RUN useradd -u 198401 nordcoderd
USER nordcoderd
```

### Verified code
```dockerfile
FROM ubuntu:20.04
RUN useradd -u -l 198401 nordcoderd
USER nordcoderd
```