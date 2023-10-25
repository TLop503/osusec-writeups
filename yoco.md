### 10/23/2023

# Yoco

### 1.
Part 1 was pretty straightforward, but it took some time to figure out. Since we have the ability to XOR an input, we can use this to determine the key being used to encrypt the flag. Inputting a long string of "A"s will return an encrypted version of this string. Since XOR is reversible via XOR, we can just XOR the output with the input. This gives us the key. XORing the encrypted flag returns the flag in plaintext. (note that there were some transitions to and from hexadecimal, I've left them out for brevity).

### 2.
Part 2 was a fair bit trickier, but a coach basically talked us through the solution after we struggled for a bit. We are given the encrypted flag and can tell via the source code that the key being used is only 4 chars long, so the encryption is wrapped. Since we know the flag likely starts with `osu{`, we can XOR this with the first chunk of the eflag to determine the key. from there, we can xor the entire eflag with the key (via cyberchef) to get the plaintext key.

### 3.
Part 3 was hard. While I understand each step logically, I was already burnt out from work in the morning and an hour of struggling to grapple with docker for the NSA challenge, so I was pretty much fried by this point. To add insult to injury, I forgot to write my file before closing after limping through Vim for the evening, so I'm running off of memory here. The flag has been encrypted using an otp that has been mixed and chained to create a much more annoying and allegedly secure otp(ttp?). However, we are given a chance to encrypt something with each key on its own. We can use this to determine each of the original otps, and then mix them again to use the process from [Part 1](1.) to access the key. We handled this all programmatically, as well as a bunch of converting to and from hexadecimal. I miss web challenges, and thinking is hard.
