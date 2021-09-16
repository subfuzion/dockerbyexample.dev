---
title: "Time"
weight: 30
---

Navigate to the `basics/time` directory in the examples repo.

Take a look at the `get-time.sh` bash script.

<!-- markdownlint-disable -->
{{< tabpane >}}
{{< tab header="get-time.sh" lang="bash" >}}
#!/bin/bash

# Ref: See section on Daytime Protocol
# https://www.nist.gov/pml/time-and-frequency-division/time-distribution/internet-time-service-its

# first arg is frequency, default is 5 seconds
freq=${1:-5}
echo "Fetch UTC(NIST) time every ${freq} seconds..."

while true; do
  if dt=$(cat </dev/tcp/time.nist.gov/13 | tail -n 1); then
    if [[ "$dt" =~ .*"UTC(NIST)".* ]]; then
      d=$(echo "$dt" | cut -d " " -f 2)
      t=$(echo "$dt" | cut -d " " -f 3)
      echo "$d $t"
    fi
  fi
  sleep "${freq}"
done
{{< /tab >}}
{{< /tabpane >}}
<!-- markdownlint-restore -->

Using a loop, this program reads a TCP socket on a Linux-based system for
fetching the current time from the [NIST Internet time
service](https://www.nist.gov/pml/time-and-frequency-division/time-distribution/internet-time-service-its)
and prints a formatted version of the response to the terminal.

The program accepts an argument specifying the frequency for fetching the time
in seconds, defaulting to 5 if not provided.

You can test the program on your own machine.

```text
chmod +x get-time.sh
./get-time.sh 1
```

<!-- markdownlint-disable -->
{{< tabpane >}}
{{< tab header="Output" lang="text" >}}
Fetch UTC(NIST) time every 1 seconds...
21-09-02 18:15:02
21-09-02 18:15:03
21-09-02 18:15:04
21-09-02 18:15:12
^C
{{< /tab >}}
{{< /tabpane >}}
<!-- markdownlint-restore -->

<!-- markdownlint-disable --> 
{{% pageinfo %}}
&#x1F632; **Note**

If this doesn't work on your machine, don't worry, you've
just experienced one of the big reasons why containers are so useful!

Continue to the next page to containerize the time app so we can run it in a
standard Linux environment that will work everywhere Docker is supported.
{{% /pageinfo %}}
<!-- markdownlint-restore -->
