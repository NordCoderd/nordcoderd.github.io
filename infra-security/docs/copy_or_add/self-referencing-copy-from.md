---
layout: default
title: "Dockerfile: Avoid Self-Referencing COPY --from Instructions"
permalink: /infrastructure-security/self-referencing-copy-from
tags: ["plugin", "maintainability", "docker"]
---

### Problem
Using `COPY` with the `--from` flag to reference the current build stage is not allowed. This mistake leads to build errors and confusion.

### Description
The `COPY` instruction with the `--from` flag must refer to a previous build stage. Referencing the current stage alias is invalid because you cannot copy from the image you are currently building.

### Solution
Do not use the current stage alias with the `--from` flag. Instead, reference only previous stages when copying files.

### Problematic code
```dockerfile
FROM ubuntu:20 as builder
USER nobody
RUN apt-get update && apt-get install --no-install-recommends -y build-essential

# Incorrect: referencing the current build stage "builder"
COPY --from=builder /app /app
```

### Verified code
```dockerfile
FROM ubuntu:20 as builder
USER nobody
RUN apt-get update && apt-get install --no-install-recommends -y build-essential

FROM ubuntu:20
USER nobody
# Correct: referencing the previous build stage "builder"
COPY --from=builder /app /app
```