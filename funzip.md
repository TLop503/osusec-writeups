# Funzip

## Context stuff
Json Web Tokens are encrypted tokens stored as cookies containing json files with information about the user. For example, a token might include a user's name, and where their files are stored on a server. Usually they have some extra protections to make it harder to exploit, but ctf league is chill.  
Symlinks are "symbolic links" that act like pointers to files. They can be included in zip files and can point to whatever they want, even if it doesn't exist.

## Solution
Poking around the source code reveals that the public key for the encryption used for signing jwt's is stored on the server. Uploading a symlink to this file lets us read it, gaining access to the key needed to sign our own JWTs. Decoding a JWT we have from the site cookie lets us see that it has an "admin" property, that we can set to true and re-sign. Now, we can access the site's status page, which includes the uid for the admin account. Since we know from the src that the flag is stored at /uid/flag.txt, we can upload another symlink and read the flag.

## Here be dragons...
Since we have the admin uid and the ability to write new tokens, this lets us impersonate the admin account. Zane is patching this, but one could theoretically arbitrarily overwrite the admin dir.
