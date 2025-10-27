---
title: "Custom Fonts"
description: "For WP Bricks builder, may work with other builders too."
date: 2025-03-14
# image: ""
lastmod: 2025-03-14
showTableOfContents: true
tags: ["WordPress", "Bricks"]
type: "post"
---

I found a video by [Matty Eastwood](https://www.youtube.com/@mr.matt.eastwood) on how to upload `Custom Fonts` with Bricks Builder.

If you uploaded custom fonts before with Bricks Builder, I am sure you understand the hassle to upload the fonts.
But Matty showed us an easier way to upload custom fonts with a few different ways of how to do it.

You can watch the full video [here](https://www.youtube.com/watch?v=I9L9NG2y_W0).

I will use the plug-in method by [altmann.de](https://www.altmann.de/en/blog-en/code-snippet-custom-fonts/).

## 1. Install Plug-In

Note, that this is not your typical plug-in, it is very lightweight in code and does not affect your site speed.

Go to this [blogpost](https://www.altmann.de/en/blog-en/code-snippet-custom-fonts/) of his, scroll down and you will find a source code.

Create a folder, Copy the code and save it as `custom-fonts.php` then upload into the plug-in folder you created. Then, when you activate it, it will do it's magic.

## 2. Download Fonts

I use <https://webfontloader.altmann.de/> to download Google Fonts.

## 3. Upload Fonts

Extract the downloaded file, remove unnecessary documents that comes with the downloads, then upload in the `wp-content/uploads/fonts` folder.

I prefer to use much more modern and lightweight WOFF2 format.


> - *Post Changelogs*
>   - *28th Oct - 2025 - Added font upload.*
