---
title: "Dockerfile with both"
linkTitle: "Combining both!"
weight: 3
---

What if we want to override the container to behave the way it does with an
`ENTRYPOINT`, but we want to override the default frequency of `5` seconds?

You use *both* `ENTRYPOINT` and `CMD`.

<!-- markdownlint-disable -->
{{< tabpane >}}
{{< tab header="Dockerfile.using_both" lang="docker" >}}
FROM debian
COPY get-time.sh /usr/local/bin
RUN chmod +x /usr/local/bin/get-time.sh
ENTRYPOINT [ "/usr/local/bin/get-time.sh" ]
CMD [ "2" ]
{{< /tab >}}
{{< /tabpane >}}
<!-- markdownlint-restore -->

Rebuild the Docker image.

```text
docker build -f Dockerfile.using_entrypoint -t get-time .
```

Run a container.

```text
docker run -it --rm --name timectr get-time
```

<!-- markdownlint-disable -->
{{< tabpane >}}
{{< tab header="Output" lang="text" >}}
Fetch UTC(NIST) time every 2 seconds...
21-09-02 19:30:53
^C
{{< /tab >}}
{{< /tabpane >}}
<!-- markdownlint-restore -->

What happens here is that the value for `CMD` acts as a default argument that
will be passed to the command specified by `ENTRYPOINT`. You can still pass an
argument when you create the container and it will just override `CMD`'s default
value.

```text
docker run -it --rm --name timectr get-time 3
```

<!-- markdownlint-disable -->
{{< tabpane >}}
{{< tab header="Output" lang="text" >}}
Fetch UTC(NIST) time every 3 seconds...
{{< /tab >}}
{{< /tabpane >}}
<!-- markdownlint-restore -->
