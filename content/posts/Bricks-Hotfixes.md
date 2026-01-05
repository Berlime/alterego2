---
title: "Bricks Hotfixes"
description: "Quick fixes and setup tips for Bricks Builder"
date: 2026-01-05
lastmod: 2026-01-05
type: "post"
showTableOfContents: true
tags: ["WordPress", "bricks",]
---

I wanted a single spot for the Bricks fixes I reach for most often, so I merged my setup, checkout padding, anchor link, and checkbox tweaks into this quick notebook. If you are curious about how I prep posts like this, peek at [My reference when publishing a blog](/posts/my-reference-when-publishing-a-blog).

## 1. Bricks, ACSS, Frames Setup

### Why this stack
Bricks + Automatic.css (ACSS) + Frames is still my fastest path to a styled build. The automatic setup flow is fine when I am in a hurry, but I always keep the manual steps ready in case the import files change.

### Prerequisites

- Bricks Builder installed and activated.
- Automatic.css 2.1+ (ACSS 4.x works too).
- Frames plugin download from my account.
- Ability to upload SVGs in Bricks (at least for admins).

### ACSS setup (automatic)

1. Import the Bricks Settings JSON into `Bricks > Settings`.
2. Import the Bricks Theme JSON into `Bricks > Settings > Theme Styles`.
3. In Theme Styles, assign the style to the whole site (Conditions tab).
4. Optional but helpful after import:
   - Typography: set body/headings font and push HTML font size to `var(--root-font-size)`.
   - Container width: `var(--content-width)`.
   - Performance: leave “Disable class chaining” ON and load CSS as Inline Styles.
5. Manual fallback when import files change:
   - `Bricks > Settings`: SVG uploads on for admins, disable Bricks OG/SEO meta tags, add element IDs when needed, Remote Templates set to Frames (`https://bricks.getframes.io`, password = Frames license).
   - Builder: Disable element spacing, Dynamic data render ON, Global Class Import set to Never.
   - Theme Styles: assign site-wide, set the defaults above, leave other globals empty to avoid conflicts.

Reference: https://docs.automaticcss.com/builder-configuration/how-to-setup-acss-with-bricks-builder

### Frames setup

1. Install and activate Frames (ACSS must already be active).
2. Activate the license at `Automatic CSS > Frames License` (non-bundle key).
3. Enable SVG uploads for Bricks (admin scope is fine).
4. Add remote templates at `Bricks > Settings > Templates > Remote Templates` using:
   - URL: `https://bricks.getframes.io`
   - Password: Frames license key
5. In the ACSS Dashboard flip:
   - Frames > Load Frames Styling: ON
   - Frames > Components: ON (recommended)
   - Spacing > Smart Spacing: ON
6. Open any page or template in Bricks and confirm remote templates appear.

Reference: https://getframes.io/docs/installing-activating-frames/

### Verify

- Drop a Frame from Remote Templates inside the Bricks editor and confirm styling matches ACSS tokens.
- Inspect computed styles: container width should reflect `var(--content-width)` and the root font size should follow ACSS.
- Confirm Bricks keeps class chaining disabled in Performance settings.

## 2. Archive templates

This is a good video I found to create `Archive Templates` with WordPress's native `Blog/Post Page`, `Categories Page` etc.

The video tutorial is especially good if you want multiple CPT's archive page to look the same.

In my case, I create a Single template that is used for `Posts` archive page and `Post Category` archive page.

<https://www.youtube.com/watch?v=tWl3Oxn-Zs8&t=142s>

## 3. Checkout Page Fix

### When to use this
When the WooCommerce checkout template sits inside narrow theme padding, everything feels cramped and the order summary either overlaps or floats way too low. This global CSS patch frees the canvas without touching templates or recreating the layout in Bricks.

### Capture the checkout wrapper ID

1. Open the published checkout page (not the builder preview).
2. Inspect the `body` element and note the WordPress generated class (e.g. `post-202` or `page-id-87`).
3. That class scopes the spacing so the rest of the site stays untouched.

### Drop the global CSS

Add the snippet below to your global styles (Bricks > Settings > Custom Code > CSS, ACSS Global Styles, wherever you keep universal CSS). Swap `post-###` for the class you copied above.

```css
/* Checkout Page replace [#] (e.g; post-202) to your specific ID by inspecting */
.post-### {
  margin-block: 5rem;
  padding-inline: 2rem;
  max-width: 100%;
}

.alignwide {
  width: 100% !important;
}
/* End-Checkout Page */

/* Start Sticky WC Summary Offset Padding */
@container (min-width: 700px) {
  .wc-block-checkout__sidebar {
    align-self: flex-start;
    top: 4rem !important; /* Cant Use Var */
  }
}
/* End Sticky WC Summary Padding */
```

### Why it works

- `.post-###` widens the checkout canvas and gives it breathing room without touching other templates.
- `.alignwide` forces Bricks wide containers to truly span the available width.
- The container query only fires when the sidebar sits beside the form, keeping the order summary pinned 4 rem from the top so it never jumps on scroll.

### Quick QA

1. Resize between 640–1024 px to confirm the container query only kicks in on wider layouts.
2. Scroll through a long order; the sidebar should stay offset but never overlap the footer.
3. Revisit other templates to confirm their original padding stays intact (the body class scoping prevents bleed).

## 4. Anchor Links

Creating anchor links in Bricks is straightforward. I just set an ID on the target section and link to it.

### Set up the target section

1. Select the section you want to link to.
2. Go to **Style > CSS > CSS ID**.
3. Set an ID (example: `my-section`).

### Create the link

1. Select the button or text element that should jump.
2. Set the Link type to **External URL**.
3. For the URL, enter `#my-section` (hash followed by your ID).

The link now jumps to that section. If you want smooth scrolling, flip the option inside **Bricks Settings**.

Reference: https://forum.bricksbuilder.io/t/solved-how-to-make-an-anchor-link/342/2

## 5. Form Checkbox Alignment

The default Bricks form checkbox layout tends to misalign the label and input. Dropping the snippet below inside the form’s CSS (use `%root%` so it scopes to the form component) keeps everything neat.

```css
%root% ul.options-wrapper li {
  display: flex;
  align-items: flex-start;
  gap: 10px;
}

%root% ul.options-wrapper input {
  margin-top: 6px;
}
```

Reference: https://forum.bricksbuilder.io/t/bricks-form-how-to-align-checkbox-label/24818

If any of these tweaks help, just drop me a note at kamil@berlime.com, I am around.

> - *Post Changelogs*
>   - *05 Jan 2026 - Publish Date - Combined multiple short posts about bricks*
