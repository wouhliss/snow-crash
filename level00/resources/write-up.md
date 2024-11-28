# Level00 Write-up

## Objective:

The goal of this level was to explore the system and find a hidden flag to progress further.

## Step-by-step process:

### Step 1: Searching for Suspicious Files

To start, I explored the file system using the following command to list all files recursively and look for any potential flags:

```bash
ls -lRah / 2> /dev/null | grep flag00
```

This revealed a potential lead: flag00 was associated with the string john.

### Step 2: Locating the File

Next, I used the find command to locate where `john` was stored:

```bash
find / -name "john"
```

This pointed me to the path: /usr/sbin/john.

### Step 3: Reading the File

After finding the file, I inspected its contents by running:

```bash
cat /usr/sbin/john
```

The output was: cdiiddwpgswtgt.

### Step 4: Decrypting the String

The string cdiiddwpgswtgt looked encrypted, and I suspected it was a Caesar cipher. Using a ROT15 decryption, the string decrypted to:

`nottoohardhere`
