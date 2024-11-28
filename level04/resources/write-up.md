# Level04 Write-up

## Objective:

The goal of this level was to exploit a web service running on the local machine to execute a command and retrieve the flag.

## Step-by-step process:

### Step 1: Analyzing the Web Service

I discovered that a web service was running on port `4747` on the local machine. I used `curl` to interact with it:

```bash
curl localhost:4747
```

The web service was a CGI-based Perl script that accepted a parameter `x`. This led me to investigate whether the `x` parameter could be used to inject a command.

### Step 2: Exploiting the Web Service

After identifying the potential command injection point, I attempted to execute the `getflag` command by passing it as the value for the `x` parameter:

```bash
curl localhost:4747/?x='$(getflag)'
```
