---
title: "Free Up Space Ubuntu"
date: 2024-12-17
description: "Free disk space on Ubuntu 24.04: clear APT cache, remove old kernels, and keep the system updated, often reclaims hundreds of MB to a couple of GB."
image: ""
lastmod: 2026-02-19
showTableOfContents: true
tags: ["server", "dev",]
type: "post"
---

Running low on disk on Ubuntu 24.04? This is my quick “get space back fast” checklist: APT cache, old kernels, then a clean update/upgrade cycle. On a typical box this can free ~500MB–2GB, depending on how long it’s been since you cleaned up.

Before and after, check your free space:

    df -h

**Quick reference (copy/paste)**

    du -sh /var/cache/apt/archives
    sudo apt-get clean
    sudo apt-get autoremove --purge
    sudo apt update && sudo apt upgrade

## 1. Clear the APT Cache

Every `apt install`/upgrade can leave cached `.deb` files behind. That cache often grows quietly over time and is one of the easiest wins to reclaim space from.

Find out how large the APT package cache is:

    du -sh /var/cache/apt/archives

Clear the cache:

    sudo apt-get clean

## 2. Remove Old Kernels

After kernel updates, older kernel packages can stick around so you can boot a previous version if needed. `autoremove --purge` removes unused packages (including old kernels) that are no longer required.

Proceed with caution (especially if you’ve pinned kernels or you’re in the middle of troubleshooting boot/driver issues):

    sudo apt-get autoremove --purge

## 3. Last, stay up to date

Do this regularly. Keeping packages current reduces stale dependencies and keeps your system in a healthier state.

    sudo apt update && sudo apt upgrade

Check your free space again:

    df -h

More tips (and the original source I grabbed these from): [5 ways to free up space on Ubuntu](https://www.omgubuntu.co.uk/2016/08/5-ways-free-up-space-on-ubuntu).

> - *Post Changelogs*
>   - *17th Dec 2024 - Publish Date*
>   - *19th Feb 2026 - Add context + quick reference, fix upgrade command*