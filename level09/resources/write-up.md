# Level09 Write-up

## Objective:

The goal of this level was to decode a flag that was encoded using a custom rotation scheme, which was similar to a ROT cipher.

## Step-by-step process:

### Step 1: Analyzing the Encoding Scheme

The binary provided in this level encoded the flag using a rotation technique. However, the exact encoding method was not directly visible, so I deduced the logic based on the behavior of the binary.

From the binary's behavior, I realized that each character in the flag was being adjusted based on its position in the string, similar to a rotation cipher. Specifically, the character's ASCII value was being modified by subtracting its index from the ASCII value of the character.

### Step 2: Replicating the Decoding Logic

After deducing the encoding method, I replicated it in Python. The decoding process involved reversing the operation by adding the index to the ASCII value of each character:

```python
char = raw_input()
a = ""
for i in range(len(char)):
    a += str(chr((ord(char[i]) - i)))
print(a)
```

### Step 3: Decoding the Flag

I used a similar Python script to decode the contents of the `token` file:

```bash
cat token | python -c 'char = raw_input()
a=""
for i in range(len(char)):
    a += str(chr((ord(char[i]) - i)))
print(a)'
```
