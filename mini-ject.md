### 10/16

# Mini-ject or little bobby tables

Today was the first SQL injection web challenge. Admittedly someone else in my team found the flag while at a different table, so this is more of a breakdown of their solution. The target is a simple website whith a list of posts filtered so that only posts with the bool private set to false are showed. There is a filter box that presumably runs  

``` SELECT FROM posts WHERE varchar LIKE <input>; ```

Since our target is posts flagged as private, we need to either list all private posts or just list all posts. A way to work around this would be to manipulate the selection to show posts that meet the condition OR true = true, so as to dump every post. The tricky thing with this is that the end of the string still exists in the query. To avoid this, we can use

```"OR""="```

Breaking this down:

`"OR` Escapes the input and opens an or. We need the other side to evaluate to true.

`""="` "The empty string equals `"`. This opens a logical check if the empty string is equal to the start of another empty string. Normally this wouldn't work, but the end of the expected input supplies the end of the quotes. So overall the query reads:

``` SELECT FROM posts WHERE varchar LIKE "" OR "" = "" AND private = false;```

Logically, this shouldn't really work because the private flag is still being checked. Weirdly, this query works and dumps the flag. Adding a comment to the end of the query still works too.
