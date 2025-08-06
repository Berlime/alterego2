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

## Clean WP Post Meta Table (DB) 

Back Up Database before performing this action.

https://www.youtube.com/watch?v=iqIw3aHKZWY
[https://Orbisius.com/yt7274](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbTJIR2RzaEJhX2dycVgySGRpalNZUDlZcExRUXxBQ3Jtc0tscDZCRFdjTnJYVjJuUzhuZ2J6RHRKZFRMSGZtMkUwb09SRUVFUzl6YTdUN0M3bFJzV1VCZWZoYXVUX2g5dGliN2pPYnVtTkpXbmNTNEIxOU8xRXZKV0VGOVZGSHFfQjl5OHZHOTYwR1E5TnRWVkRxNA&q=https%3A%2F%2FOrbisius.com%2Fyt7274&v=iqIw3aHKZWY)

### Instructions

Back up your database before performing this action.

1. Log-in into phpMyadmin.
2. Select the ‘database’, then click the ‘SQL’ tab.

```sql
// Assuming that your table prefix is the default one: wp_ 
// If you're using a different one update the queries as needed.
// The selec funtion will show how many empty values are stored in the post meta table.

SELECT * FROM `wp_postmeta` WHERE meta_value='' OR 
SELECT * FROM `wp_postmeta` WHERE meta_value IS NULL

// Execute one line at a time.

// Then, click 'Edit inline', remove the current query, and replace with..

DELETE FROM `wp_postmeta` WHERE meta_value=''
DELETE FROM `wp_postmeta` WHERE meta_value IS NULL

.. You want all the columns that store exactly the number 0. No more, no less.

SELECT * FROM `wp_postmeta` WHERE meta_value REGEXP '^[0]$';

// Delete all rows that have meta_value field column as 0.

DELETE FROM `wp_postmeta` WHERE meta_value REGEXP '^[0]$';
```

> - *Post Changelogs*
>   - *14th Jan 2025 - Publish Date, find Elementor Field*
