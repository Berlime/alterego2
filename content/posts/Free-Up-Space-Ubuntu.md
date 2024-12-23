---
title: "Free Up Space Ubuntu"
date: 2024-12-17
description: "Ubuntu 24.04"
# image: ""
lastmod: 
showTableOfContents: true
tags: ["server", "dev"]
type: "post"
---

## 1. Clear the APT Cache

Find out how large is the apt package cache:

    du -sh /var/cache/apt/archives

Clear the cache:

    sudo apt-get clean

## 2. Remove Old Kernels

Not sure how it works, really but here we go,

Proceed with caution:

    sudo apt-get autoremove --purge

## 3. Last, stay up to date

Do this regularly

    sudo apt update && upgrade

You can read the full article where I found the above commands [here](https://www.omgubuntu.co.uk/2016/08/5-ways-free-up-space-on-ubuntu).

> - *Post Changelogs*
>   - *17th Aug 2024 - Publish Date*