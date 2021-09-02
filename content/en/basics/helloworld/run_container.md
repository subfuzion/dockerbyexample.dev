---
title: "Run a container"
weight: 40
---

Now that you have an image, you can launch a container to run your program.

```text
docker container run --rm hello
```

<!-- markdownlint-disable -->
{{< tabpane >}}
{{< tab header="Output" lang="text" >}}
Hello, world!
{{< /tab >}}
{{< /tabpane >}}
<!-- markdownlint-restore -->

The `--rm` option tells Docker to remove the container once the process
running in it terminates. It's generally a good idea to clean up resources
when no longer needed.

One reason not to automatically remove a container when the running process
terminates is to inspect the logs after.

```text
docker container run --name helloctr hello
```

You'll see the same the output as before. This time we gave the container a
name using the `--name` option to make it easy to refer to it. You can
inspect everything the process wrote to `stdout` and `stderr` with the
`docker logs` command.

```text
docker container logs helloctr
```

<!-- markdownlint-disable -->
{{< tabpane >}}
{{< tab header="Output" lang="text" >}}
Hello, world!
{{< /tab >}}
{{< /tabpane >}}
<!-- markdownlint-restore -->

The logs show the same output that was printed to the terminal.

Even though the process exited and the container is no longer usable,
you can see that it still exists with the `docker container ls` command.



```text
docker container ls --all
```

<!-- markdownlint-disable -->
{{< tabpane >}}
{{< tab header="Output" lang="text" >}}
CONTAINER ID   IMAGE  COMMAND       CREATED          STATUS                      PORTS      NAMES
c038996a5e75   hello  "/hello.sh"   20 seconds ago   Exited (0) 18 seconds ago              helloctr
{{< /tab >}}
{{< /tabpane >}}
<!-- markdownlint-restore -->

The `--all` option was needed to show containers that have exited.

You can remove the container with the `docker container rm` command.

```text
docker container rm helloctr
```

<!-- markdownlint-disable -->
{{< tabpane >}}
{{< tab header="Output" lang="text" >}}
helloctr
{{< /tab >}}
{{< /tabpane >}}
<!-- markdownlint-restore -->

The output indicates the name of the container that was removed.

The program accepts a name argument. You can supply arguments to the `docker
run command` when you run a container.

```text
docker container run --rm hello Docker
```

<!-- markdownlint-disable -->
{{< tabpane >}}
{{< tab header="Output" lang="text" >}}
Hello, Docker!
{{< /tab >}}
{{< /tabpane >}}
<!-- markdownlint-restore -->

<!-- markdownlint-disable --> 
{{% pageinfo %}}

The original versions of the `docker container` commands are still available
and can be used as convenient shortcuts.

```text
docker container run   =>  docker run
docker container logs  =>  docker logs
docker container ls    =>  docker ps
docker container rm    =>  docker rm
```
{{% /pageinfo %}}
<!-- markdownlint-restore -->
