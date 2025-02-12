---
layout: default
title: "Dockerfile Security: Avoid Curl Bashing - Do Not Pipe to Shell"
permalink: /infrastructure-security/curl-bashing-detected
tags: ["plugin", "security", "docker"]
---

### Problem
Using `curl` or `wget` with a pipe (|) or redirection (>) to execute scripts directly poses a security risk.

### Description
Piping the output of `curl` or `wget` directly to a shell runs untrusted scripts without review. This practice can lead to the execution of malicious code in your container. It is safer to download and verify the script before executing it.

### Solution
Download the script to a file, verify its integrity, and then execute it. Avoid piping `curl` or `wget` output directly to the shell.

### Problematic code
```dockerfile
FROM ubuntu:20.04
USER nobody
RUN curl -sSL http://example.com/script.sh | sh
```

### Verified code
```dockerfile
FROM ubuntu:20.04
USER nobody
RUN curl -sSL http://example.com/script.sh -o script.sh
# run only if downloaded script was verified
```
