---
title: "Dockerfile with CMD"
linkTitle: "Using CMD"
weight: 1
---

In the Dockerfile for the previous example, you used the `ENTRYPOINT`
instruction to specify the process to execute in the container. This time you'll
use the `CMD` instruction instead and then explore the differences between the
two.

<!-- markdownlint-disable -->
{{< tabpane >}}
{{< tab header="Dockerfile.using_cmd" lang="docker" >}}
FROM debian
COPY get-time.sh /usr/local/bin
RUN chmod +x /usr/local/bin/get-time.sh
CMD [ "/usr/local/bin/get-time.sh" ]
{{< /tab >}}
{{< /tabpane >}}
<!-- markdownlint-restore -->

Build a Docker image to run this.

```text
docker build -f Dockerfile.using_cmd -t get-time .
```

Since Docker looks for `Dockerfile` by default and you're going to try using a
few different Dockerfiles, you need to use the `-f` option to be explicit about
which one to use for the build.

Now print the time using a container.

```text
docker run -it --rm --name timectr get-time
```

<!-- markdownlint-disable -->
{{< tabpane >}}
{{< tab header="Output" lang="text" >}}
Fetch UTC(NIST) time every 5 seconds...
21-09-02 19:28:45
21-09-02 19:28:51
{{< /tab >}}
{{< /tabpane >}}
<!-- markdownlint-restore -->

We used a new option for the `docker run` command: `-it`. This is actually a
combined option using two short flags, `-i` and `-t`. The first allows us to
pass input to the container over `stdin`; the second attaches a pseudo-terminal,
which means for one thing it can respond to the `SIGINT` signal when you press
`Ctrl-C` on your keyboard to terminate the process.

The container appears to behave the same way as when we used `ENTRYPOINT`
before. However, one difference is that `CMD` acts more like a default. You
can easily override the default command, as shown below.

```text
docker run -it --rm --name timectr get-time echo hello
```

<!-- markdownlint-disable -->
{{< tabpane >}}
{{< tab header="Output" lang="text" >}}
hello
{{< /tab >}}
{{< /tabpane >}}
<!-- markdownlint-restore -->

The `get-time.sh` script is no longer executed; instead, the command `echo` with
the argument `hello` was executed in the container. Since the base image for the
`get-time` image was `debian`, the standard `echo` command exists in the path
when the container is launched.

Because the argument that you provide in the `docker run` command replaces the
default command, you can't just provide the frequency option like this (since
there is no `2` command).

```text
# this won't work!
docker run -it --rm --name timectr get-time 2
```

Instead, you need to supply the entire command to override the default one:

```text
docker run -it --rm --name timectr get-time get-time.sh 2
```

<!-- markdownlint-disable -->
{{< tabpane >}}
{{< tab header="Output" lang="text" >}}
Fetch UTC(NIST) time every 2 seconds...
21-09-02 19:29:42
21-09-02 19:29:44
^C
{{< /tab >}}
{{< /tabpane >}}
<!-- markdownlint-restore -->

Since `/usr/local/bin` is in the path for the `debian` image, it wasn't
necessary to fully qualify the path for `get-time.sh`. The fully-qualified
path was used in the `CMD` instruction is often a good practice for clarity.

Let's revisit using `ENTRYPOINT` next.
