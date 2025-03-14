---
title: "SQL Command"
description: "Useful tricks to navigate database in phpMyAdmin"
date: 2025-01-14
# image: ""
lastmod: 2025-01-14
showTableOfContents: true
tags: ["dev", "WordPress",]
type: "post"
---

## Elementor field

Particularly with the `<p>` tag.
In this case, I have stopped subscribing to Elementor Pro which made my slider template gone, including the content.

Elementor does not allow you to view the content in the admin area without renewing the license.
However, it seems that the content is still available in the database, and below is to comment to find contents you insert with the Elementor elements.

```sql
SELECT * FROM `wp_posts` WHERE post_content LIKE '%<!-- wp:paragraph -->%';
```

- Replace `'wp_posts'` to whatever database you want to find from.
- Replace `post_content` to filter through the columns in the table.
- Replace `'%<!-- wp:paragraph -->%'` to find the content, be sure that it starts and ends with ` % `.

https://nitropack.io/blog/post/wordpress-database-cleanup-guide

> - *Post Changelogs*
>   - *14th Jan 2025 - Publish Date, find Elementor Field*
