# Level13 Write-up

## Objective:

The goal of this level was to reverse-engineer the binary and find the password by analyzing the `ft_des` function.

## Step-by-step process:

### Step 1: Analyzing the Binary with Ghidra

I started by using **Ghidra** to reverse-engineer the `level13` binary. In the disassembly, I found a function called `ft_des`, which was used to transform the string `"boe]!ai0FB@.:|L6l@A?>qJ}I"`.

### Step 2: Understanding the `ft_des` Function

By analyzing the code of the `ft_des` function in Ghidra, I realized that I needed to find out what the function would return when passed the string `"boe]!ai0FB@.:|L6l@A?>qJ}I"`. This function seemed to perform some kind of transformation or decryption.

### Step 3: Replicating the Function Locally

To find the output of `ft_des("boe]!ai0FB@.:|L6l@A?>qJ}I")`, I copied the code of the `ft_des` function from Ghidra and ran it locally.
