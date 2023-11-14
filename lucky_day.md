### 11/13/23
# Lucky Day (OSINT 1)

Part 1:
In the challenge you are given the user's github username. We can use the .patch trick to identify their email. There is a comment in a file on their repo mentioning they have a flickr account with the same username as their email. Checking their flickr has screenshots of their tweets, which gives us the username and the first flag.

Part 2:
The user's tweets include an encrypted flag, as well as mentions to vignere and using their username for the key. Using this information we can decrypt the key into a base64 string (as detected by cyberchef). Converting base64 into standard ascii/utf8 gives us the second flag.
