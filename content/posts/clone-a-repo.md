---
date: 2025-09-12T16:39:28+08:00
lastmod: 2025-09-12
showTableOfContents: true
title: Clone a Repo
type: post
tags:
  - dev
  - github
---
## My set up for cloning themes.

I first fork a repo into my own GitHub account, then I clone that forked into my local environment.

I then create these branches:

1. Main - I don't change any code in this main branch, the reason being if there is any updates from the repo owner, I can easily bring in the updates.
2. Live - This branch will be the branch that is final
	1. Some cases, i created another branch for special development by adding a suffix of `-hostinger` in this case, it is a label on what hosting/server I use. Particularly for Hostinger, this branch only have the public/dist folder.
3. Development - This is where I make changes. After I have completed and tested it, this will merge onto the `Live` repo.

