# Log Search Tool

## Description

This is a tool that lets you search files for keywords, provided that the keywords are 4 characters or longer. You have to use this to "search the logs and discover what the attackers were after"

Hint: "Always search deeper"

-----

## Notes/Initial Thoughts

- It would be great if we could view the entire contents of a file. How?
  - We can bypass the character limit on the client side, but it looks like they check on server side too
- We can use url `/file=<filename>&term=<term>` for easier testing
- In the `hostnames.txt` file, we can search ".com" and find 5 results
  - One of these is a valid hostname: "update.ourhobby.com". This site looks super sus, is this part of the challenge?
- Maybe you can use regex to search?
  - nah don't think so
- In the javascript files, searching for stuff like "html", "script", or "var " will get results, but not the whole thing.
- I think that we could rebuild the entire hex dump by searching for stuff like "0000", "0001", etc... but is that worth the effort?