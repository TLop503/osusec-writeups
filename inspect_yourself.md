### 10/9/23
# Inspect_yourself_1 - 3

The first web challenge of the year, and luckily this one was fairly straightforward. Right off the bat, using devtools/inspect element reveals a comment in the html body listing the first flag. Poking around a bit more, I noticed the site loads a cookie called "notflag" (subtle). This was a seemingly random string of letters and numbers, but someone in my team noticed that it ends with an equals sign. We used an online decoder to revert this back into the second flag. At this point the website was temporarily down, so I wasted some time on red herrings, before it came back up. The officers had mentioned common filepaths that may be public, such as /robots.txt or /security.txt. Security didn't return anything useful, but robots listed the following:

````
User-agent: Google-Extended
Disallow: /flag
Disallow: /other
````

/flag had a lot of important information, but /other ended up containing the flag. I already had devtools open, but the flag was stored in plaintext with white font on a white background for extra security. Overall this was a fun challenge, definitely a lot easier than last week's binary exploitation. It'll be interesting to see how the season progresses.

This writeup feels uncomfortably simmilar to canvas discussion posts I have to make each week, lol.
