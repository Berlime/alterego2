---
title: "JetEngine"
description: "I copied this from my Notion notes."
date: 2025-01-10
# image: ""
lastmod: 2025-02-01
showTableOfContents: true
tags: ["WordPress",]
type: "post"
---

## Introduction

This is my notes when using JetEngine with Bricks. I reference to this a lot to fit into my context and at least for my thought processes.

## Repeater Fields

Use Listings/Components by JetEngine to accommodate repeater field loop sin the front end, be sure that the name is the same with the italicized `name id`.

Then include in the Single Post Template, use JetEngine widget.

You can also use native Bricks template system, which does not require JE's Listings/Components.
To populate in Bricks, set the query to `JE Repeater` it will populate available repeater for the particular Brick's `single` template in the `Template Setting`.

---

## Meta Box

From WordPress Dashboard, hover to `JetEngine` > `Meta Boxes`

- Ability to assign custom fields to `any type of content` (e.g. CPT, post, users, categories, pages.)
- Ability to add custom fields to built in WordPress post types (e.g. posts, users, categories, pages etc.)
- Structure Hierarchy > Meta Box Name > Meta Fields.
- Ability to add additional to custom field to Taxonomy

> 💡
>
> #1 Use case: add additional data in Customers in Users.
>
> #2 Use case: Able to add Galleries in Category/Taxonomies.
>
> Useful video tutorial
>
> <https://www.youtube.com/watch?v=fa1ezuf7HUQ&list=PLTbrc9HXDstrLg449hcWQvx8kOXhjyovV&index=4>

---

## Listings

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

---

## Components

Able to create components to be used in different places throughout the website. Especially great if the components have dynamic data enabled.

---

## Glossaries

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

---

## Query Builder

Query builder is when you have a set of customized data to pull in a listing or an archive page. You can pull from multiple data types (e.g. CPT, CCT, core WordPress posts and even databases). It also allows you to stack the queries, meaning it is not tied to a single data sets like a CPT.

> Here is an overview video of query builder by Paul C <https://www.youtube.com/watch?v=n8YmsTLHuRU>

At the moment with Bricks builder, if you turn on custom query, the other query fields on the left sidebar won't work as the custom query will override them.

### Show Related Item in SPT

> Here is a great tutorial video of building query by Crocoblock <https://www.youtube.com/watch?v=ZB9gE7JAMAs&t=410s>

1. For this, it may be slightly different from what builder you use.
2. Note if the items you want to show is `parent` or `children`.

### Query Post Metadata

In this section, the goal is to be able to select Internal Pages URL dynamically from a CPT's meta-field.

1. Create a post query like in the screenshot

![query-screenshot](/images/PostMetaData.avif)

2. Then in your CPT meta-field: Define the Value Field and Label Field.

![screenshot](/images/queryPostMetaData2.avif)

### Nested Query

In a Single Post Template, I want to display the meta-data of the `related items`. In this case, I want to display the form title, the `form` itself is another CPTs.

1. Go to the `Query Builder` > Scroll to `Post Query` section > `Post Page` > `Post In` > `Initial Object ID From (get initial ID here)` must be set to `Current object variable`.

## Taxonomies

This is when you want to create a category or tags for your CPT.

When you edit a post, you can select categories with a checkbox. To enable this in the admin area, you need to turn on `Hieraricle` JetEngine settings.

If you want to select like a `tag` style experience, simply turn off the `Hieraricle` settings which is turned off by default.

Be sure to input the `Capability Type` to category, this will trigger to display in Admin UI.

It was used base on this
<https://wordpress.org/documentation/article/roles-and-capabilities/>

Do not forget to use the Admin filters & admin columns in JetEngine settings when you have a lot of data.

---

## Admin Columns

This is very interesting, not only that you can display your `CPT meta data` in the admin area of your CPT. You can also display the `relations` in the admin column.

1. In the "type" section, select `Custom Callback`.

![screenshot](/images/jetengineAdminColumns.avif)

2. Then, in the "Callback" section, click `Select from existing callbacks`

![screenshot](/images/jetengineAdminColumns1.avif)

3. Click on the highlighted text in the `Get related items`.

![screenshot](/images/jetengineAdminColumns3.avif)

4. Select an option, and you are done!

![screenshot](/images/jetengineAdminColumns4.avif)

## Note when using with Bricks

1. In Bricks builder, you need to turn on Query Loop, then you can choose a Post Type. You can also query multiple Post type.

    This solves the problem when I want to:-

    - Create `two different post types` showing the `same metadata`.
    - `Create different CPT` instead of `categories or taxonomies`, for ease of use for clients.
    - Reduce clicks for non-technical users to create new post.

> - *Changelogs*
>   - *1st Feb 2025 - Added Admin Columns*
>   - *17th Jan 2025 - Added Taxanomies and Bricks Notes*
>   - *24th Jan 2025 - Added context in Meta Box*
