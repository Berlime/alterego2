---
title: "I use Hugo for this blog"
date: 2024-01-30
description: "Another noob perspective"
# image: ""
lastmod: 2025-01-15
showTableOfContents: true
tags: ["blog", "dev", "static",]
type: "post"
---

## Hugo is a static site generator

Introduced by my good friend of mind back in Secondary school. I straight away fell in love in static sites. I have been dabbling into WordPress thinking that it is the 'Holy Grail' of web development. *buzzz!!* Nope. I was totally wrong.

Tasnim, actually first started using [Hugo](https://gethugo.io) for his own personal blog. He thought me a lot about how VS Code works, this is the point where I discovered the term IDE, he is darn good at explaining complex things into simple terms. Which struck me like a lightning.

Hugo is also easy to get start with well documented tutorials. It has exciting themes to choose from. And here I landed with a theme called Gokarna.

*Shout out to [Avijit Gupta](https://buymeacoffee.com/avijitgupta) for such a great work and the other author and [contributors](https://github.com/gokarna-theme/gokarna-hugo)!

The footer of this blog, and the image remains as to credit the huge amount of work for those who create this theme which is perfect and simple at least according to my design needs.

## Image Uploads

I recently discovered how to upload Images in my [rounded corners](/rounded-corners).

Here is briefly how,

For some reason, we need to add the following in the config file, in my case it's `hugo.toml`

```toml
  [[module.mounts]]
  source = 'images'
  target = 'static/images'
```

Then, in the `markdown` file of your post, 

```markdown
![screenshot](/images/roundedcorners2.avif)
```

Just be sure that the `target` file path is where your images is.


> - *Changelogs*
>   - *15th Jan 2025 - Image Uploads*
>   - *27th Dec 2024 - Fixed context*
>   - *29th Oct 2024 - Publish Date*
