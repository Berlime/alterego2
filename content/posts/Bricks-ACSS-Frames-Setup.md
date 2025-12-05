---
title: "Bricks, ACSS, Frames set up"
description: "Concise setup notes for Bricks Builder with Automatic.css and Frames"
date: 2025-12-05
lastmod: 2025-12-05
showTableOfContents: true
tags: ["WordPress"]
type: "post"
---

## Why this stack

Bricks + Automatic.css (ACSS) + Frames is a fast way to ship Bricks sites with consistent styling and ready-made layouts. This post uses the automatic setup flow for ACSS but manual setup is safer when plugin updates land or if you know what you are doing.

## Prerequisites

- Bricks Builder installed and activated.
- Automatic.css 2.1+ (ACSS 4.x is fine).
- Frames plugin download from your account.
- Ability to upload SVGs in Bricks (turn on for admins).

## ACSS setup (automatic)

This is the quickest way to align Bricks defaults to ACSS. For projects that might receive plugin updates soon, keep the manual steps handy in case the import files change.

1) Import Bricks Settings file (JSON) into `Bricks > Settings`.  
2) Import Bricks Theme file (JSON) into `Bricks > Settings > Theme Styles`.  
3) In Theme Styles, assign the style to the whole site (Conditions tab).  
4) Optional but recommended defaults after import:
   - Typography: set your body/headings font; set HTML font size to `var(--root-font-size)`.
   - Container width: `var(--content-width)`.
   - Performance: keep “Disable class chaining” ON; CSS loading Inline Styles.
5) If you prefer manual setup (good fallback when import files change), mirror the doc settings for:
   - Bricks > Settings: SVG uploads on for admins; Disable Bricks OG/SEO meta tags; Add element ID as needed; Remote Templates set to Frames (`https://bricks.getframes.io`, password = Frames license).
   - Builder: Disable element spacing; Dynamic data render ON; Global Class Import set to Never.
   - Theme Styles: assign site-wide; set defaults noted above; leave other globals empty to avoid conflicts.

Reference: https://docs.automaticcss.com/builder-configuration/how-to-setup-acss-with-bricks-builder

## Frames setup

1) Install and activate Frames plugin (requires ACSS active).  
2) Activate license at `Automatic CSS > Frames License` (use the non-bundle key).  
3) Enable SVG uploads for Bricks (admin at minimum).  
4) Add remote templates: `Bricks > Settings > Templates > Remote Templates`  
   - URL: `https://bricks.getframes.io`  
   - Password: Frames license key  
5) In ACSS Dashboard:  
   - Frames > Load Frames Styling: ON  
   - Frames > Components: ON (recommended)  
   - Spacing > Smart Spacing: ON  
6) Open any page/template in Bricks and confirm Remote Templates are available.

Reference: https://getframes.io/docs/installing-activating-frames/

## Verify

- In Bricks editor, add a Frame from Remote Templates and check styling matches ACSS tokens.
- Inspect computed styles: container width should reflect `var(--content-width)`, root font size from ACSS.
- Confirm no class chaining in generated CSS (Bricks performance setting).

---

> - *Post Changelogs*
>   - *05 Dec 2025 - Initial publish*

