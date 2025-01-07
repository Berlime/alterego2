---
title: "Regex"
description: "First Encounter With Regex"
date: 2025-01-07
# image: ""
lastmod: 2025-01-07
showTableOfContents: false
tags: ["Dev", "WordPress",]
type: "post"
---

Previously, I posted about [Woo Commerce Products Add-Ons](/WCPA) on using a formula to determine the value of a wood radius that needs to be cut.

Today, while developing a client's site, I realize that phone number fields requires some special characters like '()' and "+" and of course spaces.

I use CoPilot to create for me that Regex, and my prompt was:

```markdown
Give me an example of a regex pattern that includes symbols
```

To create a regex pattern that allows alphanumeric characters, specific symbols like @, #, $, %, and &, as well as spaces, you can use the following pattern:

```bash
^[a-zA-Z0-9@#$%&\s]+$
```

Here's the breakdown of the pattern:

- `^` asserts the position at the start of the string.

- `[a-zA-Z0-9@#$%&\s]` matches any letter (both uppercase and lowercase), digit (0-9), the specified symbols (`@`, `#`, `$`, `%`, `&`), or a whitespace character (`\s`).

- `+` ensures that the pattern occurs one or more times.

- `$` asserts the position at the end of the string.

This pattern will match any string that contains a mix of the allowed letters, digits, symbols, and spaces.

> - *Post Changelogs*
>   - *7th Jan 2025 - Publish Date*
