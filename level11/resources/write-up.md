# Level11 Write-up

## Objective:

The goal of this level was to exploit a Lua script running on a server, allowing us to execute a command and retrieve the flag.

## Step-by-step process:

### Step 1: Connecting to the Server

The first step was to connect to the service running on `localhost` using `nc` (Netcat) on port `5151`:

```bash
nc localhost 5151
```

### Step 2: Identifying the Exploit

Once connected, I realized the Lua script was using `io.popen` to execute commands. This function allows running shell commands from within Lua and capturing the output. The script was vulnerable to command injection through user input.

### Step 3: Exploiting the Lua Script

To exploit this vulnerability, I injected the `getflag` command by passing it as input to `io.popen` in the following manner:

```lua
io.popen('echo "..pass.."')
```

I modified the `pass` variable to inject the `getflag` command. The exploit was executed as follows:

```lua
password; getflag > /tmp/token
```

This caused the Lua script to execute the `getflag` command and store the result in `/tmp/token`.

### Step 4: Retrieving the Flag

After executing the exploit, I retrieved the flag by reading the contents of the `/tmp/token` file:

```bash
cat /tmp/token
```
