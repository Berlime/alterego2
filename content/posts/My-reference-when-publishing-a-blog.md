---
title: 'My Reference When Publishing a Blog'
description: "This blog loads faster than my PC opening up the note app."
date: 2024-12-27
# image: ""
lastmod: 2024-12-27
showTableOfContents: true
tags: ["static", "dev"]
type: "post"
---

## Create New Post via Terminal

1. Make sure you are at `/your_site`

    ```bash
    hugo new content/posts/my-first-post.md
    ```

    or simply edit your current blogpost at `content/post/your-post.md`

2. Save the file and go to terminal, cd to `/your_site` and run the command `hugo` to regenerate public files

    ```bash
    hugo
    ```

3. Now let git check the changed file using this in `/your_site`

    ```bash
    git status
    ```

    it should display something like this

    ```bash
    Changes to be committed:
      (use "git rm --cached <file>..." to unstage)
            new file:   .gitmodules
            new file:   themes/gokarna

    Untracked files:
      (use "git add <file>..." to include in what will be committed)
            .hugo_build.lock
            archetypes/
            content/
            hugo.toml
            pub
    ```

4. At `/public`, add the files, commit (make sure at the selected branch) then push

    ```bash
    git add .
    # to add all files

    git commit -am "commit message"
    # commit with a message

    git push origin test-branch
    # push the new files to the Origin(URL) <branch name>
    ```

5. For the `master` branch, repeat step 4 in `/gokarna`

## Deployment

For now, I deploy manually due to Feather Icons having issues loading the SVG.

### Manual Deployment

1. Deploying via SFTP:
    1. Delete these folders and upload the new ones (Do not upload the `.git` folder):
        - `robots.txt`
        - `index.xml`
        - `404.html`
        - `sitemap.xml`
        - `index.html`
        - `posts`

    > 💡 **Note:** Deleting all files in `public_html` and then uploading the new ones will not work. To identify which folders need an update, in FileZilla, sort the files by "Last Modified". You will see the latest date the changes happened. Those are the files that should be replaced.

> - *Post Changelogs*
>   - *27th Dec 2024 - Publish Date*
