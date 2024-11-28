# Level06 Write-up

## Objective:

The goal of this level was to exploit a vulnerability in a PHP file to execute arbitrary code and retrieve the flag.

## Step-by-step process:

### Step 1: Crafting the Payload

From the analysis of the program, I discovered that the executable used `preg_replace` with the `\e` modifier, which allowed execution of PHP code within a pattern. I crafted a malicious payload to exploit this behavior by injecting a command to execute `getflag`.

I created the following payload and saved it in a file:

```bash
echo '[x {${exec(getflag)}}]' > /tmp/test
```

This payload would inject and execute the `getflag` command when processed by the `preg_replace` function with the `\e` modifier.

### Step 2: Executing the Program

Next, I passed the crafted file `/tmp/test` as input to the `level06` executable:

```bash
./level06 /tmp/test
```
