---
layout: default
title: "Dockerfile Security: Avoid Exposing Ports Outside Allowed Range"
permalink: /infrastructure-security/exposed-port-out-of-range
tags: ["plugin", "security", "docker"]
---

### Problem
Exposed port is out of range. Ports must be within 0-65535.

### Description
The Dockerfile declares an exposed port that falls outside the valid UNIX port range of 0-65535. Using an invalid port number is a misconfiguration that may cause errors during build or runtime.

### Solution
Use a port number within the range of 0-65535 in the `EXPOSE` instruction.

### Problematic code
```dockerfile
FROM ubuntu:20.04
USER nobody
EXPOSE 70000
```

### Verified code
```dockerfile
FROM ubuntu:20.04
USER nobody
EXPOSE 8080
```