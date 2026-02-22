---
title: "I use Hugo for this blog"
date: 2024-01-30
description: "Another noob perspective"
# image: ""
lastmod: 2025-01-15
showTableOfContents: true
tags: ["blog", "dev", "static",]
type: "post"
---

## Hugo is a static site generator

Introduced by my good friend of mind back in Secondary school. I straight away fell in love in static sites. I have been dabbling into WordPress thinking that it is the 'Holy Grail' of web development. *buzzz!!* Nope. I was totally wrong.

Tasnim, actually first started using [Hugo](https://gethugo.io) for his own personal blog. He thought me a lot about how VS Code works, this is the point where I discovered the term IDE, he is darn good at explaining complex things into simple terms. Which struck me like a lightning.

Hugo is also easy to get start with well documented tutorials. It has exciting themes to choose from. And here I landed with a theme called Gokarna.

*Shout out to [Avijit Gupta](https://buymeacoffee.com/avijitgupta) for such a great work and the other author and [contributors](https://github.com/gokarna-theme/gokarna-hugo)!

The footer of this blog, and the image remains as to credit the huge amount of work for those who create this theme which is perfect and simple at least according to my design needs.

## Image Uploads

I recently discovered how to upload Images in my [rounded corners](/posts/rounded-corners/).

Here is briefly how,

For some reason, we need to add the following in the config file, in my case it's `hugo.toml`

```toml
  [[module.mounts]]
  source = 'images'
  target = 'static/images'
```

Then, in the `markdown` file of your post,

```markdown
![screenshot](roundedcorners2.avif)
```

Just be sure that the `target` file path is where your images is.

---

## Collapsible Element

I initially use this to create an expandable/collapsible section for long codes.

My prompt in DeepSeek was `In Hugo, how do I create a collapsable markdown element?`

In Hugo, you can create a collapsible Markdown element using HTML within your Markdown content. Since Markdown itself doesn't support collapsible sections, you can use the `<details>` and `<summary>` HTML tags to achieve this functionality.

Here's how you can do it:

### 1. Using HTML in Markdown

   You can directly embed HTML in your Markdown files. Use the `<details>` and `<summary>` tags to create a collapsible section.

   ```markdown
   ## My Section

   This is some regular Markdown content.

   <details>
     <summary>Click to expand</summary>
     This content is hidden by default. It will be shown when you click the summary.
   </details>
   ```

   When rendered, this will create a collapsible section with the text "Click to expand". Clicking on it will reveal the hidden content.

### 2. Styling the Collapsible Section

   You can add custom CSS to style the collapsible section. For example, you might want to change the appearance of the `<summary>` element.

   ```markdown
   <details>
     <summary style="cursor: pointer; color: blue; font-weight: bold;">Click to expand</summary>
     This content is hidden by default. It will be shown when you click the summary.
   </details>
   ```

### 3. Using Shortcodes (Optional)

   This is the method that I use.

   If you find yourself using collapsible sections frequently, you can create a custom shortcode in Hugo to simplify the process.

   - Create a file named `collapsible.html` in the `layouts/shortcodes/` directory.
   - Add the following content to the file:

     ```html
     <details>
       <summary>{{ .Get 0 }}</summary>
       {{ .Inner }}
     </details>
     ```

   - Now, you can use the shortcode in your Markdown files like this:

      ```markdown
      {{</* collapsible "Click to expand" */>}}
      This content is hidden by default. It will be shown when you click the summary.
      {{</* /collapsible */>}}
      ```

<!-- If you want to display the code for the shortcode usage without it being rendered in the front end, you can use Hugo's {{</* */>}} syntax to escape the shortcode -->

This approach allows you to reuse the collapsible section structure easily across your conten and works well in Hugo and is compatible with most modern browsers.

---



> - *Changelogs*
>   - *29th Jan 2025 - Collapsible Element*
>   - *15th Jan 2025 - Image Uploads*
>   - *27th Dec 2024 - Fixed context*
>   - *29th Oct 2024 - Publish Date*
