---
title: "Rounded Corners"
date: 2024-12-18
description: "Utilises WCPA to the max."
# image: ""
lastmod: 2024-12-18
showTableOfContents: false
tags: ["dev", "wordpress"]
type: "post"
---

## WCPA Rounded corners for custom wood orders

First, we need to determine the minmax of the cuts for each corner. This cuts must be relative to the width and the length.
The goal is to allow users to customize order not just by adding rounded corners on the required sides, but also, allows granular measurement for irregular shapes, and routing.

## We need to start from the 4 sided measurements

First, we need to identify the mid-point variable where,

- length: {value/2}
- width: = {value/2}

With this, we now have 4 mid-points, 1 on each side.

## Determine the label of each corner

We will now need users to imagine if the longer side is perpendicular with a surface, where the longer side is standing and not laying flat.
For this, we need to display an image as HTML as a guide, on which field, false into which corner.

## Determine WCPA form context

Now we will decide if the WCPA form is handled globally or locally.

If **Global**, each field for the corner radius value will need to have a conditional logic set to, '{product,productSize,productThickness,productWidth,ProductLength}'

There are hundreds of wood products that have multiple combinations of variations. Hence, this will render the Global WCPA form obsolete as there will be so many rules involved.

To mitigate this, we will locally scope the Rounded Corners field in each product.

> - *Changelogs*
>   - *18th Dec 2024 - First Publish*
