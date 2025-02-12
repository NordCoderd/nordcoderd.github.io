---
layout: default
title: "Dockerfile: Use JSON Notation for CMD and ENTRYPOINT"
permalink: /infrastructure-security/json-notation-cmd-entrypoint
tags: ["plugin", "maintainability", "docker"]
---

### Problem
Using shell notation for `CMD` or `ENTRYPOINT` may cause incorrect parsing. This leads to unexpected behavior at runtime.

### Description
Docker supports two formats for `CMD` and `ENTRYPOINT`: shell form and JSON array form. Shell form can misinterpret arguments and cause errors. JSON notation parses each argument correctly and ensures consistent behavior.

### Solution
Use JSON notation for `CMD` and `ENTRYPOINT` instructions. This guarantees proper parsing of arguments and avoids unexpected issues.

### Problematic code
```dockerfile
FROM ubuntu:20.04
USER nobody
# Shell form may misinterpret arguments
CMD echo "Hello World"
ENTRYPOINT /usr/local/bin/start-app
```

### Verified code
```dockerfile
FROM ubuntu:20.04
USER nobody
# JSON notation ensures correct parsing of arguments
CMD ["echo", "Hello World"]
ENTRYPOINT ["/usr/local/bin/start-app"]
```