---
title: "Hello World"
weight: 20
---

Let's start simple. This example exists in the `basics/hello` directory in the
examples repo, but it's so simple you might want to create your own version by
following the instructions below.

Create a unique directory for this example, such as `hello`, and then change
directory to it.

```text
mkdir hello
cd hello
```

<!-- markdownlint-disable --> 
{{% pageinfo %}}
**Important!**
You'll create a unique directory for every example. A directory must contain
its own distinct`Dockerfile` as well as any other files (
[symbolic links](https://man7.org/linux/man-pages/man7/symlink.7.html) won't
work) that will need to be copied into the generated Docker image.
{{% /pageinfo %}}
<!-- markdownlint-restore -->

You're going to write a small program -- just a basic shell script to print the
obligatory ***Hello World*** greeting.

Next you'll write a short **Dockerfile**. You'll use the Dockerfile to build a
**Docker image** that incorporates your program.

Finally you'll use the image to launch a **container**. Your program executes
inside the container.

The container is a logical abstraction based on Linux features that simply runs
the process for your program in a way that isolates it from the rest of the
system. 
