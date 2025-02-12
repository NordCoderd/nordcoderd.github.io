---
layout: default
title: "Dockerfile Security: Avoid Potential Secrets in ENV Keys"
permalink: /infrastructure-security/possible-secrets-in-env
tags: ["plugin", "security", "docker"]
---

### Problem
Dockerfiles store potential secrets in `ENV` keys. This exposes sensitive data in the image.

### Description
Storing secrets in `ENV` keys puts them directly into the image layers. Attackers can extract these secrets if they gain access to the image. Do not hardcode sensitive data in your Dockerfile.

### Solution
Remove secret values from `ENV` instructions. Inject secrets at runtime or use secure methods like Docker secrets.

### Problematic code
```dockerfile
FROM ubuntu:20.04
USER nobody
ENV PASSWORD=supersecret123
```
### Verified code
```dockerfile
FROM ubuntu:20.0
USER nobody
# Remove sensitive data from the Dockerfile.
# Inject PASSWORD at runtime using secure methods.
```