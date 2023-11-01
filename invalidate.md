### 10/30
# Invalidate (rev 1)

## Flag 1:
To start with flag 1 I cracked open the exe in Ghidra and noticed that it was a simple, OTP style encrpytion. Since I figured the first challenge was supposed to be easy, I tried entering my string as `osu{` to see how it would be encrypted, since I assumed the key would be the flag. This returned `****m`. From here I assumed that since XOR functions are reversible, if the start of the flag becomes `****`. then `*****************` would become the flag. Plugging this in returned the flag, plus the start of the flag a second time since the key wrapped.

## Flag 2:
This was rough. Revving the code revealed (with a lot of help) that input was checked first if the first character was divisible by 7, and then the rest was XOR'd into oblivion upon itself. Since this is a finite set you could brute force things at this point by automatically chekcing every option that fits these criteria, as only a few options would both start with a %7able character and be readable, but I wasn't able to sort out how to do this effectively wihtin the time constraints. I relied pretty heavily off of the walkthrough for this section.

## Flag 3:
I understand how to theoretically solve this one, but don't know how to implement it and this week is very busy.  
We are asked for three passwords. The first is the first number seeded by rand() seeded with the current time. We could probably use pwntools to seed our own instance of rand at this time and input it, effectively cloning the source code. The next 2 numbers are both being pulled from rand() and then manipulated (forgot specifically how, I'll update this if I have time). We'd need to perform these operations ourself to get the neccessary passwords, and then input all three for the flag.

## Conclusion:
1/3 flags this week (as of Wednesday at least). Conceptually things mostly make sense, but implementation for the second challenge seems very tricky. If I have time I'll come back to these and try to write tools to crack them.
