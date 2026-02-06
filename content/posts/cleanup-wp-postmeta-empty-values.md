---
title: 'Clean Up Empty wp_postmeta Rows in WordPress (phpMyAdmin)'
description: "How to safely remove empty and zero-valued post meta via SQL. Back up your database first."
date: 2025-02-06
# image: ""
lastmod: 2025-02-06
showTableOfContents: false
tags: ["wordpress", "maintenance", "database"]
type: "post"
---

WordPress stores post custom fields and plugin data in the `wp_postmeta` table. Over time it fills with empty strings, `NULL`s, and sometimes literal `0` values left by themes and plugins—or failed saves. That bloat slows queries and increases database size. You can clean it up with a few SQL statements in phpMyAdmin.

**This is destructive SQL.** You **must** take a full database backup before doing anything below.

## Back up your database first

Export the entire WordPress database from phpMyAdmin (or your hosting panel’s backup tool). Download the `.sql` file and keep it somewhere safe. If you’re not comfortable running raw SQL, get your hosting provider or a developer to do this for you.

## Prerequisites

- Access to phpMyAdmin or another MySQL client.
- Your WordPress table prefix (default is `wp_`; check `$table_prefix` in `wp-config.php`).
- A backup you can restore from if something goes wrong.

## Step 1 – Log in to phpMyAdmin

Log in via your hosting control panel, select the database that WordPress uses, then open the **SQL** tab so you can run the queries below.

## Step 2 – Inspect empty and NULL post meta

Run a **SELECT** first to see how many rows have empty or NULL `meta_value`. phpMyAdmin will show the row count.

```sql
-- Adjust `wp_` if your table prefix is different
SELECT *
FROM `wp_postmeta`
WHERE meta_value = ''
   OR meta_value IS NULL;
```

## Step 3 – Delete empty and NULL meta_value rows

Run these **one at a time**. After each, check the “affected rows” count and briefly test a few posts on the site.

```sql
DELETE FROM `wp_postmeta`
WHERE meta_value = '';
```

```sql
DELETE FROM `wp_postmeta`
WHERE meta_value IS NULL;
```

## Step 4 – Optionally remove meta rows that are exactly 0

This targets rows where `meta_value` is **exactly** the character `0` (no `10`, `0.0`, etc.). Some plugins intentionally store `0` as a valid value, so this step is optional and riskier—only do it if you’re comfortable.

First, see what would be deleted:

```sql
SELECT *
FROM `wp_postmeta`
WHERE meta_value REGEXP '^[0]$';
```

Scan the `meta_key` column for anything that looks important (e.g. plugin options). If you’re happy to remove those rows:

```sql
DELETE FROM `wp_postmeta`
WHERE meta_value REGEXP '^[0]$';
```

### Using a custom table prefix

If your `$table_prefix` in `wp-config.php` is not `wp_`, replace `wp_postmeta` in every query with your prefix, e.g. `wpabc_postmeta`.

### If something goes wrong

If the site breaks (missing custom fields, plugin errors), restore the database from the backup you made before running any of these queries.

## References

- [Orbisius – YouTube / tutorial link](https://Orbisius.com/yt7274)
- [YouTube – Back Up Database before performing this action](https://www.youtube.com/watch?v=iqIw3aHKZWY)

This post is my personal reference/summary of that method. I’d run this cleanup after removing heavy plugins or on a staging copy first.

> - *Post Changelogs*
>   - *6 Feb 2025 – Initial publish*
