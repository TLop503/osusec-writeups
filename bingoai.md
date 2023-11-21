### 11/20/23
# BingoAI (Cookies, Web, XSS, etc)

1. Part 1 requires you to read the source code. It shows that a proper login attempt creates a specific admin cookie to stay logged in. If we give ourself the same cookie, the flag is displayed on an admin page.

2. The second part is simmilar to zipservice.md - you insert data and then it gets proccessed with some extra stuff added. The field opens your request, but with unique http headers. Using beeceptor as the target, we can see what these headers are and find the flag.

3. Part 3 is broken, but there is an unsanitized textbox. Since things are run off a bot account, we are likely looking for a cookie the bot has. Using this XSS injection dumps a list of the bot's cookies:
```js
<script>
  var cookies = document.cookie.split(';');
  for (var i = 0; i < cookies.length; i++) {
    alert(cookies[i].trim());
  }
</script>
```
