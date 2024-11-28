# Level08 Write-up

## Objective:

The goal of this level was to retrieve a flag from a file that could not be opened directly, so I used a symbolic link to access it.

## Step-by-step process:

### Step 1: Creating a Symbolic Link

I discovered that I could not directly access the `token` file in `/home/user/level08/`. To work around this, I created a symbolic link to the file in the `/tmp` directory:

```bash
ln -s /home/user/level08/token /tmp/super
```

This command created a symbolic link named `super` in the `/tmp` directory that pointed to the `token` file.

### Step 2: Running the Program

After creating the symbolic link, I passed it as an argument to the `level08` executable:

```bash
./level08 /tmp/super
```
