---
title: "How I Host My Main Site in Netlify and a Sub-Directory Using WordPress on a Different Server"
date: 2026-02-19
description: "How I host berlime.com on Netlify (Hugo) while serving WordPress from a different server under /guides, plus the gotchas that will bite you."
image: 'static/images/avatar.webp'
lastmod: 2026-02-19
showTableOfContents: true
tags: ["dev", "WordPress", "agency",]
type: "post"
---

My main site, `berlime.com`, lives on Netlify. I added a separate WordPress instance in a sub-directory (`/guides`) on a different server, so the main site and the guides section run on different instance.

So now my stack looks like this:

- **Netlify** for hosting and proxying
- **Astro** for the main site build
- **WordPress** running on a different server inside a sub-directory `https://berlime.com/guides`
- **WP CLI** to fix database URLs properly

## The goal

- `https://berlime.com/` to be served by Netlify
- `https://berlime.com/guides/` to load WordPress, but WordPress lives on another server (`https://wp.berlime.com`)


## How it works

Netlify serves the static site like normal.

For anything under `/guides/*`, Netlify acts like a reverse proxy and forwards the request to my WordPress server.

WordPress must be configured to believe its canonical URL is `https://berlime.com/guides`, otherwise it will constantly try to “help” you by redirecting, generating wrong links, breaking admin flows, and doing the classic WordPress thing where nothing is obviously broken but many features quietly stop working.

## Netlify config

This is the core of it, a proxy-style redirect.

In `netlify.toml`, add:

```toml
[[redirects]]
  from = "/guides"
  to = "/guides/"
  status = 301
  force = true

[[redirects]]
  from = "/guides/*"
  to = "https://wp.berlime.com/guides/:splat"
  status = 200
  force = true
```

Notes:

- That first rule is boring but important, it forces `/guides` to become `/guides/`, and keeps the query string. 

- `status = 200` is the trick here, it makes Netlify proxy the request instead of redirecting the browser.
- `force = true` is me being explicit, I do not want other rules to win.

My existing `netlify.toml` already has the Hugo build bits, so this rule just sits alongside that.

## The WordPress instance

My WordPress lives on a different server under `wp.berlime.com`.

In my case, I also keep WordPress effectively “mounted” under `/guides` on that server too, so the proxy target becomes `https://wp.berlime.com/guides/...`.

You can do it other ways, you can proxy `/guides/*` to the WordPress root and let it route internally, but I found mirroring the sub-path on the WP side reduces surprises.

## WP-Config

This is the non negotiable part.

In `wp-config.php` (on the WordPress server), define the canonical URLs like this:

```php
define('WP_HOME', 'https://berlime.com/guides');
define('WP_SITEURL', 'https://berlime.com/guides');
```

Without these, WordPress will often try to send you to `wp.berlime.com`, or it will generate admin URLs, asset URLs, and internal links that do not match your proxy path.

## Ensure wp-config respects HTTPS behind a proxy

When you proxy through Netlify, the WordPress server may see the incoming request as plain HTTP, even though the public URL is HTTPS.

That causes classic WordPress problems like mixed content, wrong redirects, cookies behaving weirdly, and login sessions that feel cursed.

In `wp-config.php`, add this as well:

```php
if (
  isset($_SERVER['HTTP_X_FORWARDED_PROTO']) &&
  $_SERVER['HTTP_X_FORWARDED_PROTO'] === 'https'
) {
  $_SERVER['HTTPS'] = 'on';
}
```

Optionally, I also like forcing admin SSL:

```php
define('FORCE_SSL_ADMIN', true);
```

## The annoying con

One con with this whole setup is that some saves in WordPress admin can trigger a reload that tries to go to:

- `https://berlime.com` (root), instead of
- `https://berlime.com/guides` (your sub-directory)

When you see that happening, it is almost always a sign that either:

- `WP_HOME` / `WP_SITEURL` are not correctly set, or
- the database still contains old absolute URLs pointing to the original domain you installed WordPress on

Which brings me to the most important part of this post.

## Fix the database URLs properly (WP CLI search replace)

This is critical:

When you install WordPress, it writes absolute URLs into the database immediately.

If you install WordPress while it is still using `https://wp.berlime.com` (before you set up the Netlify proxy and the canonical `/guides` URLs), then your database content will contain `wp.berlime.com` everywhere.

Your Netlify redirect rules do not magically rewrite existing database values.

So you need to do a proper search replace using WP CLI:

```bash
wp search-replace 'https://wp.berlime.com' 'https://berlime.com/guides' --skip-columns=guid --all-tables
```

Why I do it this way:

- `--all-tables` because WordPress installs love adding tables, plugins love adding tables, I just want it done.
- `--skip-columns=guid` because changing `guid` is generally a bad time.

After running this, a bunch of “basic” WordPress stuff that looks broken suddenly starts working again, permalink generation, media URLs, internal links, builder links, all the usual suspects.

## Etch WP plugin bug

This one was fun.

From the front end, the link came out as:

`https://berlime.com/guides?etch=magic&post_id=3610`

Notice the missing `/` before the query string. It should be:

`https://berlime.com/guides/?etch=magic&post_id=3610`

With the proxy rule `from = "/guides/*"`, the missing trailing slash means the request no longer matches the path the way you expect, so you can end up bypassing your proxy behavior entirely.

For me this showed up while using **Etch** (WordPress site builder). Once I knew what to look for, it was obvious, but it took me a while to notice that one missing character was the whole problem.

If you hit this, the quickest sanity check is to manually add the slash and see if the page suddenly behaves.

---

If this helped, just drop me a note at kamil@berlime.com, I’m around.

> - *Post Changelogs*
>   - *19th Feb 2026 - Publish Date*
