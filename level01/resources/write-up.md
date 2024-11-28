# Level01 Write-up

## Objective:

The goal of this level was to crack a password and gain access to the `flag01` user.

## Step-by-step process:

### Step 1: Inspecting the `/etc/passwd` file

I started by inspecting the `/etc/passwd` file to gather information:

```bash
cat /etc/passwd
```

This revealed the following entry for flag01:

`flag01:42hDRfypTqqnw:3001:3001::/home/flag/flag01:/bin/bash`

The second field 42hDRfypTqqnw appeared to be an encrypted password.

### Step 2: Preparing the Password for Cracking

To crack the password, I saved the encrypted string into a file using the following command:

```bash
echo -n "42hDRfypTqqnw" > file
```

### Step 3: Cracking the Password Using John the Ripper

Given the clue from the file name and the type of encryption, I decided to use _John the Ripper_, a password-cracking tool. I ran John on the file containing the password hash:

```bash
./john file
```

John successfully cracked the password, revealing it to be:

`abcdefg`
