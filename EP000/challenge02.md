# Log Search Tool

## Description

This is a tool that lets you search files for keywords, provided that the keywords are 4 characters or longer. You have to use this to "search the logs and discover what the attackers were after"

Hint: "Always search deeper"

-----

## Notes/Initial Thoughts

- It would be great if we could view the entire contents of a file. How?
  - We can bypass the character limit on the client side, but it looks like they check on server side too
- We can use url `/file=<filename>&term=<term>` for easier testing