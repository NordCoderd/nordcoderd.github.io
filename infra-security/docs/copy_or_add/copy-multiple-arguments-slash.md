---
layout: default
title: "Dockerfile: Ensure Trailing Slash for COPY Commands with Multiple Arguments"
permalink: /infrastructure-security/copy-multiple-arguments-slash
tags: ["plugin", "maintainability", "docker"]
---

### Problem
When a `COPY` command has more than two arguments, the last argument must end with a slash. Omitting the trailing slash can cause errors.

### Description
When you copy multiple files, the destination must be a directory. If the destination does not end with a slash, Docker may misinterpret it. This mistake leads to build errors or unexpected file placements.

### Solution
Append a trailing slash to the destination directory in `COPY` commands with multiple source arguments.

### Problematic code
```dockerfile
FROM ubuntu:20.04
USER nobody
COPY file1.txt file2.txt dir
```

### Verified code
```dockerfile
FROM ubuntu:20.04
USER nobody
COPY file1.txt file2.txt dir/
```