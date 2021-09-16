---
title: "Dockerfile with ENTRYPOINT"
linkTitle: "Using ENTRYPOINT"
weight: 2
---

Let's rebuild the `get-time` image using an `ENTRYPOINT`.

<!-- markdownlint-disable -->
{{< tabpane >}}
{{< tab header="Dockerfile.using_entrypoint" lang="docker" >}}
FROM debian
COPY get-time.sh /usr/local/bin
RUN chmod +x /usr/local/bin/get-time.sh
ENTRYPOINT [ "/usr/local/bin/get-time.sh" ]
{{< /tab >}}
{{< /tabpane >}}
<!-- markdownlint-restore -->

Rebuild the Docker image.

```text
docker build -f Dockerfile.using_entrypoint -t get-time .
```

Now run a container.

```text
docker run -it --rm --name timectr get-time
```

<!-- markdownlint-disable -->
{{< tabpane >}}
{{< tab header="Output" lang="text" >}}
Fetch UTC(NIST) time every 5 seconds...
21-09-02 19:30:53
^C
{{< /tab >}}
{{< /tabpane >}}
<!-- markdownlint-restore -->

So far the behavior seems the same. However, unlike with `CMD`, arguments
don't override the `ENTRYPOINT`; instead, they are passed to. This behavior is
more aligned with our expectations for containers that run specific programs.

```text
docker run -it --rm --name timectr get-time 2
```

<!-- markdownlint-disable -->
{{< tabpane >}}
{{< tab header="Output" lang="text" >}}
Fetch UTC(NIST) time every 2 seconds...
21-09-02 19:33:26
21-09-02 19:33:28
^C
{{< /tab >}}
{{< /tabpane >}}
<!-- markdownlint-restore -->
