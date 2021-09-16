---
title: "The Dockerfile"
weight: 2
---

Create a Dockerfile.

<!-- markdownlint-disable -->
{{< tabpane >}}
{{< tab header="Dockerfile" lang="docker" >}}
FROM alpine
COPY hello.sh /
ENTRYPOINT [ "/hello.sh" ]
{{< /tab >}}
{{< /tabpane >}}
<!-- markdownlint-restore -->

Build a Docker image with the following command. The trailing dot (`.`)
indicates that the path to the `Dockerfile` is the current working directory.

```text
docker build -t hello .
```

<!-- markdownlint-disable -->
{{< tabpane >}}
{{< tab header="Output" lang="text" >}}
[+] Building 8.0s (8/8) FINISHED
 => [internal] load build definition from Dockerfile                                                                 0.9s
 => => transferring dockerfile: 97B                                                                                  0.0s
 => [internal] load .dockerignore                                                                                    1.1s
 => => transferring context: 2B                                                                                      0.0s
 => [internal] load metadata for docker.io/library/alpine:latest                                                     2.6s
 => [auth] library/alpine:pull token for registry-1.docker.io                                                        0.0s
 => [internal] load build context                                                                                    0.7s
 => => transferring context: 84B                                                                                     0.0s
 => [1/2] FROM docker.io/library/alpine@sha256:e1c082e3d3c45cccac829840a25941e679c25d438cc8412c2fa221cf1a824e6a      2.1s
 => => resolve docker.io/library/alpine@sha256:e1c082e3d3c45cccac829840a25941e679c25d438cc8412c2fa221cf1a824e6a      0.3s
 => => sha256:e1c082e3d3c45cccac829840a25941e679c25d438cc8412c2fa221cf1a824e6a 1.64kB / 1.64kB                       0.0s
 => => sha256:b06a5cf61b2956088722c4f1b9a6f71dfe95f0b1fe285d44195452b8a1627de7 528B / 528B                           0.0s
 => => sha256:bb3de5531c18f185667b0be0e400ab24aa40f4440093de82baf4072e14af3b84 1.49kB / 1.49kB                       0.0s
 => => sha256:552d1f2373af9bfe12033568ebbfb0ccbb0de11279f9a415a29207e264d7f4d9 2.71MB / 2.71MB                       0.6s
 => => extracting sha256:552d1f2373af9bfe12033568ebbfb0ccbb0de11279f9a415a29207e264d7f4d9                            0.1s
 => [2/2] COPY hello.sh /                                                                                            0.7s
 => [3/3] RUN chmod +x /hello.sh                                                                                     1.2s
 => exporting to image                                                                                               0.6s
 => => exporting layers                                                                                              0.5s
 => => writing image sha256:35be16e40caf802a0fb0d7a09dca7bce970162b62635d870134e64b754c67967                         0.1s
 => => naming to docker.io/library/hello
{{< /tab >}}
{{< /tabpane >}}
<!-- markdownlint-restore -->

## What just happened?

You can see a bunch of things happened in the output. In a nutshell, the `docker
build` command submitted the `Dockerfile` and the rest of the contents of the
directory (anything that isn't ignored by a `.dockerignore` file, if present) to
the Docker daemon running on your system. Most of the output reflects the
administrative details of the process used to create the final image.

An image is composed of cacheable layers. In the output that begins with `=>
[1/3] FROM docker.io/library/alpine` we can see that Docker pulled the `alpine`
base image from the alpine repository at a remote registry (docker.io) comprised
of a number of layers that will provide the Linux distribution for our program.
This operating environment will run on top of the Linux kernel on your host
system (if you're running on a Mac or Windows machine, this will be in a virtual
machine running on your system).

For the line of output that contains `=> [2/3] COPY hello.sh /`, Docker executes
the `COPY` instruction that tells the Docker daemon to copy `hello.sh` from the
root of the build context (the set of files that the Docker CLI `docker build`
command sent to the Docker daemon) into the root (`/`) of the image.

In the line that contains `=> [3/3] RUN chmod +x /hello.sh`, Docker updates the
image by running the Linux command to set the executable bit on the program. If
you set the executable bit on the script when you tested it, it's likely that
the file was copied correctly with the bit set, but you shouldn't assume this.
Always ensure you set any permission bits explicitly.

The final `ENTRYPOINT` instruction in our Dockerfile doesn't add any layers to
the image, which is why there's no corresponding line that says `[4/4]`. It adds
metadata that is used to specify the process that want to execute when a
container is created.

## Try this

Run the `docker image ls` command:

```text
docker image ls hello
```

<!-- markdownlint-disable -->
{{< tabpane >}}
{{< tab header="Output" lang="text" >}}
REPOSITORY   TAG       IMAGE ID       CREATED          SIZE
hello        latest    1cb37f5aaa1b   2 minutes ago    5.34MB
{{< /tab >}}
{{< /tabpane >}}
<!-- markdownlint-restore -->

You can confirm that the image was created, check its size (the bulk of the
image comes from the Alpine Linux distribution), and note that the image ID
fragment (`02bcec72c45a`) corresponds with the last layer that was created.
