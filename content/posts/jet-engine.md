---
title: "JetEngine"
description: "I copied this from my Notion notes."
date: 2025-01-10
# image: ""
lastmod: 2025-01-13
showTableOfContents: true
tags: ["WordPress",]
type: "post"
---

## Dynamic Data

### Meta Box

From WordPress Dashboard, hover to `JetEngine` > `Meta Boxes`

- Add custom fields to built in WordPress post types (e.g. posts, users, categories, pages etc.)
- Structure Hierarchy > Meta Box Name > Meta Fields.
- Additional to custom field to Taxonomy

> 💡
>
> #1 Use case: add additional data in Customers in Users.
>
> #2 Use case: Able to add Galleries in Category/Taxonomies.
>
> Useful video tutorial
>
> <https://www.youtube.com/watch?v=fa1ezuf7HUQ&list=PLTbrc9HXDstrLg449hcWQvx8kOXhjyovV&index=4>

### Listings

From WordPress `Dashboard`, hover to `JetEngine` > `Meta Boxes`

- Acts like a ‘template’ for archive page from a WordPress builder, but it is based on `JetEngine`
- Also allows creating components. Like user profile widget.
- Listing Source: Not limited to Posts
- Able to manipulate elements within the queried post page to any source.

> 💡
>
> #1 Use case: add additional data in Customers in Users.
>
> #2 Use case: Able to add Galleries in Category/Taxonomies.
>
> Useful video tutorial
>
> <https://youtu.be/pHH_q4fx8g0?si=LV4_gxd42nW4Ol3q>

### Glossaries

From WordPress Dashboard, hover to `JetEngine` > `Glossaries` > `Create New`

- Generally speed up process if a metadata is used and displayed in multiple areas.
- Allows CPT to have a Meta Field with Glossaries. (Especially if the metadata will be use repeatedly)
- The goal is to simplify processes and make things much more organized and reduce point of failure when changing metadata.
- Able to select multiple entries in the front-end.
- It can be used in forms. (JetFormBuilder)

Useful video tutorial

<https://www.youtube.com/watch?v=2eZmGtLGTgk&t=12s>
> 💡
>
> Useful video tutorial
>
> <https://www.youtube.com/watch?v=2eZmGtLGTgk&t=12s>


### Query Builder

Query builder is when you have a set of customized data to pull in a listing or an archive page. You can pull from multiple data types (e.g. CPT, CCT, core WordPress posts and even databases). It also allows you to stack the queries, meaning it is not tied to a single data sets like a CPT.

> Here is an overview video of query builder by Paul C <https://www.youtube.com/watch?v=n8YmsTLHuRU>

At the moment with Bricks builder, if you turn on custom query, the other query fields on the left sidebar won't work as the custom query will override them.

### Taxonomies

This is when you want to create a category or tags for your CPT.

When you edit a post, you can select categories with a checkbox. To enable this in the admin area, you need to turn on `Hieraricle` JetEngine settings.

If you want to select like a `tag` style experience, simply turn off the `Hieraricle` settings which is turned off by default.

Do not forget to use the Admin filters & admin columns in JetEngine settings when you have a lot of data.

## Note when using with Bricks

1. In Bricks builder, you need to turn on Query Loop, then you can choose a Post Type. You can also query multiple Post type.

    This solves the problem when I want to:-

    - Create `two different post types` showing the `same metadata`.
    - `Create different CPT` instead of `categories or taxonomies`, for ease of use for clients.
    - Reduce clicks for non-technical users to create new post.


> - *Changelogs*
>   - *17th Jan 2025 - Added Taxanomies and Bricks Notes*
