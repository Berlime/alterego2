---
title: 'Clean Up Empty wp_postmeta Rows in WordPress (phpMyAdmin)'
description: "How to safely remove empty and zero-valued post meta via SQL. Back up your database first."
date: 2026-02-06
# image: ""
lastmod: 2025-02-06
showTableOfContents: false
tags: ["wordpress", "maintenance", "database"]
type: "post"
---

## Back Up Database before performing this action.

1. Log-in into phpMyadmin.
2. Select the 'database', then click the 'SQL' tab.

```php
// Assuming that your table prefix is the default one: wp_ 
// If you're using a different one update the queries as needed.
// The selec funtion will show how many empty values are stored in the post meta table.

SELECT * FROM `wp_postmeta` WHERE meta_value='' OR 
SELECT * FROM `wp_postmeta` WHERE meta_value IS NULL

// Execute one line at a time.

// Then, click 'Edit inline', remove the current query, and replace with..

DELETE FROM `wp_postmeta` WHERE meta_value=''
DELETE FROM `wp_postmeta` WHERE meta_value IS NULL

// You want all the columns that store exactly the number 0. No more, no less.

SELECT * FROM `wp_postmeta` WHERE meta_value REGEXP '^[0]$';

// Delete all rows that have meta_value field column as 0.

DELETE FROM `wp_postmeta` WHERE meta_value REGEXP '^[0]$';
```
### 💡 Here is the resources I found for this.
```
{{< youtube iqIw3aHKZWY >}}
```
Read blog post from the author here: [https://orbisius.com/blog/clean-up-wordpress-post-meta-table-from-empty-values-p7274](https://orbisius.com/blog/clean-up-wordpress-post-meta-table-from-empty-values-p7274)

> - *Post Changelogs*
>   - *Nothing Yet*