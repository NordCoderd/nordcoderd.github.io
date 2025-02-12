---
layout: default
title: "Dockerfile: Avoid Multiple HEALTHCHECK Instructions"
permalink: /infrastructure-security/multiple-healthcheck-defined
tags: ["plugin", "maintainability", "docker"]
---

### Problem
Multiple `HEALTHCHECK` instructions in a single stage are confusing and error-prone.

### Description
A Dockerfile should define only one `HEALTHCHECK` per stage. Using more than one leads to unpredictable behavior. It becomes unclear which healthcheck is active, making maintenance harder.

### Solution
Consolidate health checks into a single `HEALTHCHECK` instruction. Remove any extra `HEALTHCHECK` commands from the same stage.

### Problematic code
```dockerfile
FROM ubuntu:20.04
USER nobody
HEALTHCHECK --interval=30s CMD curl -f http://localhost/ || exit 1
HEALTHCHECK --interval=30s CMD wget -q -O- http://localhost/ || exit 1
```

### Verified code
```dockerfile
FROM ubuntu:20.04
USER nobody
HEALTHCHECK --interval=30s CMD curl -f http://localhost/ || exit 1
```