# Level07 Write-up

## Objective:

The goal of this level was to exploit an environment variable to execute a command and retrieve the flag.

## Step-by-step process:

### Step 1: Analyzing the Executable with Ghidra

I began by analyzing the `level07` executable using **Ghidra** to understand its behavior. I discovered that the program echoed the value of the `LOGNAME` environment variable.

### Step 2: Crafting the Exploit

Since the program used the `LOGNAME` environment variable, I exploited this by setting the `LOGNAME` variable to the output of the `getflag` command. I did this by running the following command:

```bash
export LOGNAME='$(getflag)'
```

This command set the `LOGNAME` environment variable to the flag by executing the `getflag` command and capturing its output.

### Step 3: Running the Program

With the environment variable set, I ran the `level07` executable:

```bash
./level07
```
