---
title: "ACSS"
description: "Everything ACSS & ACSS+WC"
date: 2025-01-21
# image: ""
lastmod: 2025-01-10
showTableOfContents: true
tags: ["wordpress",]
type: "post"
---

## Autogrid

### Variable Method

Downside - Uses default aggressive value, unable to pixel perfect control.

### Recipe Method with Custom Class

Link to recipes - [ACSS Recipes](https://automaticcss.com/docs/grid-recipes/)

```css
@auto-grid
```

<https://www.youtube.com/watch?v=uPBrrobHm8o&t=776s>

---

## Woo Dashboard Template

For some reason, we will need a workaround to use `Frames` and `ACCS` for WooCommerce main dashboard details, and it's child.

Here is the video from the developer I search in the ACCS's Circle community.

<https://video.tobiashaas.dev/recordings/tdVDMssbPOc0TbOmBZth>

---

## Fix Allowed HTML Tags

Frames tends to have it's own HTML tags which needs to use the PHP funcitons to allow the tags, in order for some `data-attributes` to work particularly for WooCommerce

Here is the snippet

```PHP
add_filter( 'bricks/allowed_html_tags', function( $allowed_html_tags ) {
    
    // Define the additional tags to be added (e.g. 'form' & 'select')
    $additional_tags = ['form'];
    
    // Merge additional tags with the existing allowed tags
    return array_merge( $allowed_html_tags, $additional_tags );
    
    }
);
```

Source: <https://community.automaticcss.com/c/bricks/bricks-1-10-3-breaks-quantity-field-dynamic-tags-only>

> - *Post Changelogs*
>   - *10th Feb - Woo Dashboard Template*
