---
title: "Bricks Checkout Page Fix padding issue"
description: "Global CSS that frees up the WooCommerce checkout canvas and keeps the order summary sticky inside Bricks."
date: 2025-12-05
lastmod: 2025-12-05
showTableOfContents: false
tags: ["WordPress", "bricks"]
type: "post"
---

## When to use this
When the WooCommerce checkout template sits inside narrow theme padding, the form feels cramped and the summary widget either overlaps or floats too low. This patch keeps everything global—no template overrides, no custom bricks layout.

## Step 1 – Capture the checkout wrapper ID

1. Open the published checkout page in your browser (not the builder preview).
2. Inspect the `body` element and note the WordPress-generated class (e.g. `post-202` or `page-id-87`).
3. That class scopes the checkout-only spacing so other templates stay untouched.

## Step 2 – Drop the Global CSS

Add the snippet below to your global stylesheet (`Bricks > Settings > Custom Code > CSS`, ACSS Global Styles, or wherever you keep universal CSS). Replace `post-###` with the class you copied above.

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

## Step 3 – Why it works

- `.post-###` widens the entire checkout canvas and gives it breathing room without touching other templates.
- `.alignwide` forces Bricks’ wide containers to truly span the available width (Bricks sometimes caps them at theme defaults).
- The container query only fires when the sidebar actually displays beside the form, keeping the order summary pinned 4 rem from the top so it never jumps on scroll.

## Step 4 – Quick QA

1. Resize between 640–1024 px to confirm the container query only kicks in on wider layouts.
2. Scroll an order with many fields; the `.wc-block-checkout__sidebar` should stay offset but never overlap the footer.
3. Revisit other templates to verify they keep their original padding (the body class scoping prevents bleed).

Need hands-on help? Grab a slot: https://outlook.office365.com/book/meeting@berlime.com/s/Tyovt-rHPU6N6IQ7EPVEFg2

