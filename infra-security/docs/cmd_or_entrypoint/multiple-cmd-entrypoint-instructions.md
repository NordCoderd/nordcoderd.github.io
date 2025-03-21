---
layout: default
title: "Dockerfile: Avoid Multiple CMD or ENTRYPOINT Instructions"
permalink: /infrastructure-security/multiple-cmd-entrypoint-instructions
tags: ["plugin", "maintainability", "docker"]
---

### Problem
A Dockerfile must have one `CMD` and one `ENTRYPOINT` instruction. When multiple instructions exist, only the last one takes effect, which can cause unexpected behavior.

### Description
Defining multiple `CMD` or `ENTRYPOINT` instructions creates confusion. Only the final instruction is used during container startup. This can lead to unintended commands running and make the Dockerfile harder to maintain.

### Solution
Remove duplicate `CMD` and `ENTRYPOINT` instructions. Consolidate commands into a single instruction to ensure only the intended command executes.

### Problematic code
```dockerfile
FROM ubuntu:20.04
USER nobody
# Multiple CMD instructions: only the last one is used.
CMD ["echo", "Hello"]
CMD ["echo", "World"]

# Multiple ENTRYPOINT instructions: only the last one is used.
ENTRYPOINT ["run-app"]
ENTRYPOINT ["start-app"]
```

### Verified code
```dockerfile
FROM ubuntu:20.04
USER nobody
# Single CMD instruction ensures the correct command runs.
CMD ["echo", "Hello World"]
# Single ENTRYPOINT instruction ensures the correct entrypoint runs.
ENTRYPOINT ["start-app"]
```