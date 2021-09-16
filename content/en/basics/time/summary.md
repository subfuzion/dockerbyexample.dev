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

Use `ENTRYPOINT` and `CMD` together when you want the behavior of using
`ENTRYPOINT`, but want to specify potentially more appropriate **default** 
arguments using `CMD` that will
override the containerized program's defaults. The nice thing about this
combination is that you can **still** override the `CMD` defaults when you
launch a container!

For options that should not be overridden, they should be specified as part of
the `ENTRYPOINT` instruction). Any options set using `CMD` or when running a
container will be appended to the `ENTRYPOINT` options.

Finally, as with `CMD`, you can even override the `ENTRYPOINT` when you run a
container. It just takes requires a little more work at the command line:

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

You use the `--entrypoint` option to specify the command (ex, `echo`), and then
supply an argument after the image name (ex, `hello`) as usual.
