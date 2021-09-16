---
title: "Dockerfile intro"
weight: 20
---

A [Dockerfile](https://docs.docker.com/engine/reference/builder/) is a text file
that contains instructions for building an image that defines the runtime
environment for each container launched using that image.

In the upcoming examples, you will be introduced to the following
instructions:

- [FROM](https://docs.docker.com/engine/reference/builder/#from)
- [COPY](https://docs.docker.com/engine/reference/builder/#copy)
- [ENTRYPOINT](https://docs.docker.com/engine/reference/builder/#entrypoint) and
[CMD](https://docs.docker.com/engine/reference/builder/#cmd)

`FROM`

The `FROM` instruction is used to declare the base image for the new image. This
makes it possible to compose images from other existing images that 
daisy chain the dependencies your app might require, such as:

- A language runtime, such as Node.js, that depends on another base image like
- A Linux distribution, such as Ubuntu.

`COPY`

Normally what distinguishes your image from its base image are the files that
you add to it. You might be building an image intended to be used as a more
specialized base image for yet another image, or you might be building an image
for a program that you've created and want to deploy.

Either way, you can will normally use the `COPY` instruction to copy files from
your host system into the image.

<!-- markdownlint-disable --> 
{{% pageinfo %}}
&#x1F3C6; **Best practice**

There is also an `ADD` instruction that is similar, but we won't be covering it
since using
`COPY` is preferred. See this
[best practices section](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#add-or-copy)
to learn more.
{{% /pageinfo %}}
<!-- markdownlint-restore -->

`ENTRYPOINT` and `CMD`

These instructions are used to specify the command that should be run when a
container is launched, along with any default options. There are differences
between the effect of using the two instructions, and there are reasons why
it is often ideal to use them together.

The [helloworld](../helloworld) example will introduce `ENTRYPOINT`, and the
[time](../time) example will expand and clarify both the `ENTRYPOINT` and
`CMD` instructions when used separately and together.
