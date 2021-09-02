---
title: "The shell script"
weight: 20
---

Create a simple shell script to print a greeting.

The script will print `Hello` and the name supplied as the script's first
argument (defaulting to `World` if none).

<!-- markdownlint-disable -->
{{< tabpane >}}
{{< tab header="hello.sh" lang="bash" >}}
#!/bin/sh

NAME=${1:-world}
echo "Hello, $NAME!"
{{< /tab >}}
{{< /tabpane >}}
<!-- markdownlint-restore -->

Set the executable bit and run the script in your terminal.

```text
chmod +x hello.sh
hello.sh
```

<!-- markdownlint-disable -->
{{< tabpane >}}
{{< tab header="Output" lang="text" >}}
Hello, world!
{{< /tab >}}
{{< /tabpane >}}
<!-- markdownlint-restore -->

Try the script passing a name as an argument.

```text
hello.sh Docker
```

<!-- markdownlint-disable -->
{{< tabpane >}}
{{< tab header="Output" lang="text" >}}
Hello, Docker!
{{< /tab >}}
{{< /tabpane >}}
<!-- markdownlint-restore -->
