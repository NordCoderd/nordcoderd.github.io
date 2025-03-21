---
title: How I made Docker linter for IntelliJ IDEA (and other IDE)
date: 2025-03-21 00:00:00 -0500
---
Hi, in this post, I'm sharing my experience developing a [plugin for JetBrains IDEs](https://plugins.jetbrains.com/plugin/25413-infrastructure-as-code-iac-security-linter). This plugin helps detect security and maintainability issues in Dockerfiles like [Hadolint](https://github.com/hadolint/hadolint) but is integrated deeply into your workflow. I hope you find my journey useful and interesting.

This post will be especially interesting if:
- You’re a developer curious about creating plugins for **JetBrains IDEs**.
- You enjoy exploring new technologies and pushing your skills further.
- You’re passionate about development and love experimenting with tools — I’m sure you’ll find something valuable here!

# Motivation

Let's be honest: Dockerfile linters are not new. Similar solutions can be found in the JetBrains Marketplace. I wanted to create a user-friendly tool that integrates perfectly into your IDE without installing external binaries on your system and will be open-sourced.

I was fascinated by how plugins found and highlighted problems. I wanted to understand the processes behind it, create something cool myself, help other developers find issues faster, and improve the quality of their projects.

Of course, working on a linter is not only about writing code. You must constantly study new articles and research papers, read forums and plan new inspections, conduct your own research, perform testing, and overcome any obstacles you encounter.

# Development process

## 1. Project Setup

Of course, installing the appropriate IDE is the first and obvious step in building a plugin for JB IDE. I chose the IntelliJ IDEA Community, began exploring the documentation, and found a [solid starter template](https://github.com/JetBrains/intellij-platform-plugin-template/tree/main). Armed with the template, I created a [Git repository](https://github.com/NordCoderd/infrastructure-security) on GitHub and kicked off the development process.

## 2. Idea: Security Analysis of Infrastructure As Code

For a long time, I have wanted to create my own tool for checking Dockerfiles and other Infrastructure as Code (IaC) files. I wanted it to support multiple formats and detect vulnerabilities, misconfigurations, and deviations from best practices. Many similar tools work from the CLI and require additional setup and integration. However, I aimed to develop a plugin that works out of the box, leveraging the IDE’s built-in capabilities to the fullest.

## 3.  Looking for rulesets and analyzing competitors

Of course, the open-source world is HUGE, and I started to analyze existing tools. Two of the first ones I explored were `Trivy` and `Hadolint`, which have rich rulesets for checking Docker files. I decided to begin by implementing `Trivy` rules first and developed around 20 inspections.

I dove into each rule step by step: why it is important, how to implement it properly, and what edge cases needed to be covered. Doing that taught me how to deeply understand specifics of Docker files.

## 4. Working with Docker plugin and PSI

To better integrate my inspections into the IDE, I needed to rely on the [**Docker plugin** ](https://plugins.jetbrains.com/plugin/7724-docker) maintained by JetBrains. This plugin provides syntax highlighting and parsing capabilities for Dockerfiles.

When developing inspections, the **IntelliJ Platform** offers [**PSI (Program Structure Interface)**](https://plugins.jetbrains.com/docs/intellij/psi.html), a powerful approach that allows you to work with a file's logical structure. For example, it helps you locate specific elements, analyze them, and highlight potential issues. From the moment I built my first inspection, I realized how powerful this approach was. PSI enables you to process entire files or focus on particular elements, adapting the analysis to your needs.

## 5. Improving features

Once I had implemented all the rules from [**Trivy**](https://github.com/aquasecurity/trivy-checks/tree/main), I asked myself, _“What’s next?”_ — _“More rules, of course!”_ So, I turned to [**Hadolint**](https://github.com/hadolint/hadolint) and started working on expanding the ruleset. I carefully planned my work and even created a small roadmap for the product.

I aimed to implement more rules than **Hadolint**, but — speaking of the future — I haven’t achieved that goal yet. Creating a roadmap was much easier than reaching all the milestones. I ran into many questions that required me to dive deeper into the **IntelliJ Platform** and **Docker plugin** internals.

However, those challenges made the process even more engaging and exciting.

## 6. Testing and fighting for the stability

One of my most important lessons was that **unit tests are a must**. From the beginning, I wrote many test cases to cover my inspections and ensure everything worked correctly (I’m not joking—the coverage was solid). This significantly boosted my development speed and protected me from the scary tech debt.

But then something happened: some issues, such as compatibility problems with different versions of the IDE, couldn't be caught by unit tests. I initially adapted my plugin for version 233 and newer, but after several releases and testing on the latest version, I discovered that some inspections no longer highlighted problems.

Newer versions of the **IntelliJ Platform** had changed their approach to visiting PSI elements, which caused my code to stop working as expected. So, I had to adjust my solution to stay compatible with future updates.

# Summary and next steps

Developing plugins was even more exciting and challenging than I initially thought. But that’s exactly what keeps me constantly working on my project.

I aim to create a reliable tool that supports a wide range of IDE versions and remains helpful to developers who care about securing their infrastructure.

## Knowledge

Developing plugins and inspections is a great way to explore a specific area of the IDE and improve your expertise in a particular technology. For me, that technology was **Docker**. 

Understanding why something is considered a problem and how it can lead to errors or vulnerabilities helped me start seeing things from different angles.

But the most valuable insight I gained is that plugin development sharpens your coding skills and extends your understanding of the IDE’s internals — transforming you into a true technology Jedi. Knowing what’s under the hood of your IDE or plugin gives you access to what I like to call **“dark knowledge”** — the kind of understanding that’s invisible to most developers.

Building something from scratch and publishing it on the marketplace provides the invaluable experience you can’t get from regular software development work.

## Customer Results

Since October 2024, the plugin has been downloaded over **1600 times**. What’s especially rewarding is that this growth happened almost without any marketing.

I only mentioned the plugin once in a **Hadolint** issue discussing **IDEA integration**, made two posts on **Reddit**, and shared the link with a few colleagues.

Despite such minimal promotion, the number of downloads continues to grow steadily daily. I truly appreciate every developer who installs my solution and gives it a try.

## What's next

After **more than 10 releases** and countless bug fixes and improvements, I’ve reached one of my key milestones: I built a plugin that detects Dockerfile misconfigurations and highlights points for improvement. I also put effort into writing [documentation](https://protsenko.dev/infrastructure-security) and adding quick fixes. I continue improving the plugin whenever I see an opportunity.

I plan to continue developing the project by adding more inspections and cool features. But for now, I want to shift some of my focus to another important part of product development—promotion and community building.

I want to reach more developers who can share their feedback, use the tool daily, and help me grow a small community around it.

**Community is crucial** for open-source products. Initially, you’re the only one maintaining the project, but to make it truly valuable, you need people who will use it and support its growth. Without real users, any product risks becoming a tool built **by one person for one person**. I don’t want that. I want to create a tool **for people** — something developers rely on daily.

If you want to support the project, you can [**star the repository**](https://github.com/NordCoderd/infrastructure-security), and most importantly — **share your feedback**.

**See you soon!**
