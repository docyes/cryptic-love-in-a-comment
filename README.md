# cryptic love in a comment
An example of performing sentiment analysis on comments from the latest hacker news posts using the [crul](https://crul.com) map/expand engine.

```bash
open https://news.ycombinator.com/news
|| filter "(nodeName == 'A') and (parentElement.attributes.class == 'subline')"
|| open $attributes.href$
|| filter "(attributes.class == 'comment')"
/* comment out to process all comments */
|| head 10
|| prompt "label the sentiment of this comment as either one of the following seductive, off-putting or neutral: $innerText$" 
   --enrich
|| rename
  _previous.location.href url
  _previous.innerText comment
  response sentiment
  --table "url,comment,sentiment"
|| lowercase sentiment
```
