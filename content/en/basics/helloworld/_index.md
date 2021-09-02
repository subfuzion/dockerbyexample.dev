---
title: "Hello World"
weight: 10
---

Let's start simple. This example exists in the `basics/helloworld` directory in
the examples repo, but it's so simple you might to create your own version by
following the instructions below.

Create a unique directory for this example, such as `hello`, and then change
directory to it.

```text
mkdir helloworld
cd helloworld
```

<!-- markdownlint-disable --> 
{{% pageinfo %}}
**Important!**
You'll create a unique directory for every example. A directory must contain its
own unique `Dockerfile` and any other source files that you will embed (copy)
into the image.
{{% /pageinfo %}}
<!-- markdownlint-restore -->

You're going to write a small program -- just a basic "Hello, world" shell
script.

Next you'll write a short Dockerfile. You'll use the Dockerfile to build a
Docker image that incorporates your program.

Finally you'll use the image to launch a container. Your program executes inside
the container.

The container is a logical abstraction based on Linux features that simply runs
the process for your program in a way that isolates it from the rest of the
system. 
