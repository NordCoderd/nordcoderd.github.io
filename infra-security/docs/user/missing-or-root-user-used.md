---
layout: default
title: "Dockerfile Security: Avoid Default, Root, or Dynamic User for Secure Containers"
permalink: /infrastructure-security/avoid-default-root-dynamic-user
tags: ["plugin", "security", "docker"]
---

### Problem
Docker images that do not set a static non-root user expose containers to risks. Using default, root, or dynamic user assignment lets attackers gain root access.

### Description
Running containers with an undefined user or with the `root` user increases the attack surface. Dynamic assignment can override the intended user and make the container vulnerable.

One important notice: this check only considers the final user specified in the Dockerfile. It is acceptable to run build operations as root if you later switch to a dedicated non-root user. 

Note that some base images may use a non-root user by default. Always verify the default user by checking the image documentation or using commands like `docker inspect`.

### Examples
- **Implicit User:** Not specifying a user makes Docker run the container with its default user. This default may be `root` or a non-root user. Attackers can override this setting.
- **Explicit Root User:** Writing `USER root` forces the container to run as root. This practice increases risk.
- **Dynamic User Assignment:** Using environment variables or runtime parameters to assign a user lets attackers change the user to root. This dynamic method lacks consistency and security.

### Solution
Always create and use a dedicated static non-root user in your Dockerfile. Avoid dynamic user assignment that can be overridden.

### Problematic Code
```dockerfile
# Example 1: Implicitly using the default user (can be overridden)
FROM ubuntu:20.04
RUN whoami
```
```dockerfile
# Example 2: Explicitly setting the user to root
FROM ubuntu:20.04
USER root
RUN whoami
```
```dockerfile
# Example 3: Dynamic user assignment via an environment variable (risky if overridden)
ARG APP_USER
FROM ubuntu:20.04
USER $APP_USER
RUN whoami
```

### Verified Code
```dockerfile
FROM ubuntu:20.04
# Create a dedicated non-root user and group
RUN groupadd --system app && useradd --system --create-home --gid app app
# Switch to the non-root user
USER app
RUN whoami
```