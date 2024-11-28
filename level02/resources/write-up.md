# Level02 Write-up

## Objective:

The goal of this level was to analyze network traffic and retrieve the password from a packet capture file.

## Step-by-step process:

### Step 1: Retrieving the `.pcap` File

To begin, I used `scp` to securely copy the `level02.pcap` file from the target system to my local machine:

```bash
scp -P 2222 level02@localhost:level02.pcap level02.pcap
```

This command specifies the port (-P 2222) and transfers the file level02.pcap from the remote user level02 to the local machine.

### Step 2: Analyzing the Packet Capture with Wireshark

Next, I opened the packet capture file in Wireshark for analysis:

```bash
wireshark level02.pcap
```

Within Wireshark, I looked for SSH authentication packets. By examining the packet stream, I was able to observe the hex bytes that corresponded to the keystrokes of the password.

### Step 3: Reconstructing the Password

From the hex data, I reversed the captured password and identified the string:

`ft_waNDReL0L`
