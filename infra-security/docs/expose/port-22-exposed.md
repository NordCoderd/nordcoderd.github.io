---
layout: default
title: "Dockerfile Security: Avoid Exposing Port 22"
permalink: /infrastructure-security/port-22-exposed
tags: ["plugin", "security", "docker"]
---

### Problem
Exposing port 22 might let attackers SSH into the container. This practice increases security risks.

### Description
Port 22 is commonly used for SSH. Exposing it in your Dockerfile may allow unauthorized SSH access to the container. Containers usually do not need SSH access. Removing this exposure reduces the attack surface.

### Solution
Remove the EXPOSE 22 instruction from your Dockerfile unless SSH access is absolutely required. Use only the necessary ports for your application.

### Problematic code
```dockerfile
FROM ubuntu:20.04
USER nobody
EXPOSE 22
```

### Verified code
```dockerfile
FROM ubuntu:20.04
USER nobody
# EXPOSE 22 removed to prevent unauthorized SSH access.
```