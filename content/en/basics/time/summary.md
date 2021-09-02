---
title: "Summary"
weight: 50
---

The `time` example introduced you to the difference between `ENTRYPOINT`
and `CMD`, and how you can use both together.

In summary, use `CMD` when you might want to run other processes in the
container. Some containers are specifically designed to make multiple tool
commands available, so using `CMD` is convenient.

Use `ENTRYPOINT` when you want a container to behave like a specific tool and
you want to easily supply arguments without inadvertently overriding the default
command.

Use `ENTRYPOINT` and `CMD` together when you want the benefit of using
`ENTRYPOINT`, but want to provide default arguments for the container that
override the containerized program's defaults.

Finally, as with `CMD`, you can even override the `ENTRYPOINT`. It just takes
requires a little more work at the command line.

```text
docker run -it --rm --name timectr --entrypoint echo get-time hello
```

<!-- markdownlint-disable -->
{{< tabpane >}}
{{< tab header="Output" lang="text" >}}
hello
{{< /tab >}}
{{< /tabpane >}}
<!-- markdownlint-restore -->

You use the `--entrypoint` option to specify the command, and then supply an
argument after the image name as usual.
