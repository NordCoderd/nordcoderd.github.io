---
layout: default
title: "Dockerfile: Avoid Duplicate Aliases in FROM Instructions"
permalink: /infrastructure-security/duplicate-aliases-in-froms
tags: ["plugin", "docker", "maintainability"]
---

### Problem
Different `FROM` instructions use the same alias. This causes build errors and makes the Dockerfile harder to maintain.

### Description
Docker requires each `FROM` instruction alias to be unique. Duplicate aliases lead to conflicts that stop the build process. They also reduce the clarity and maintainability of the Dockerfile.

### Solution
Assign a unique alias to every `FROM` instruction. This practice prevents conflicts and improves maintainability.

### Problematic code
```dockerfile
FROM ubuntu:20 as builder
RUN apt-get update && apt-get install --no-install-recommends -y build-essential

FROM node:14 as builder
RUN npm install
```

### Verified code
```dockerfile
FROM ubuntu:20 as builder-ubuntu
RUN apt-get update && apt-get install --no-install-recommends -y build-essential

FROM node:14 as builder-node
USER nobody
RUN npm install
```