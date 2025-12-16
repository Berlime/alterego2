---
date: 2025-12-16T09:43:22+08:00
# description: ""
# image: ""
lastmod: 2025-12-16
showTableOfContents: false
# tags: ["",]
title: "Batch Process Images to WebP Using Affinity"
type: "post"
tags: ["WordPress",]
---

I used to queue up a client's asset folder and play whack-a-mole with [Squoosh.app](https://squoosh.app/) just to get everything into WebP. Great pixels, awful throughput. I even flirted with Photoshop automation plus a plugin, but the setup felt like building a space program, probably a skill issue on my end, but I wasn't motivated to push through.

Canva buying Affinity came with a shiny new release, and tucked inside is a stupidly simple batch workflow. Affinity Photo (the Pixel persona) now does in one pass what took me a whole playlist before.

## Why I moved on from the old tools

- **Squoosh.app**: quality controls are lovely, yet converting 40 hero shots one by one while deploying a WordPress site is torture.
- **Photoshop + plugin**: sure, you can automate, but wrestling with plugin installs, action files, and permissions isn't worth the cognitive load for a quick marketing site build.
- **Affinity + Canva era**: the new version is way friendlier, and the Pixel persona is included for free. No subscriptions, no drama.

## My Affinity batch recipe

1. **Launch the Pixel persona**  
   `Affinity > Pixel > New Image Process > Batch Job...` drops you into the dedicated batch dialog. A pop up will appear.

2. **Load your sources**  
   The *Source* panel is painfully obvious, hit **Add**, multi-select the images you want to convert, and they stack up in the queue. You can drag more in later if you forgot any.

3. **Decide where things go**  
   In the *Output* section, point Affinity to a target folder. Tick the formats you need; multiple checkboxes means you can spit out PNGs and JPEGs alongside WebP if a client CMS is weird about uploads. AVIF still isn't on the menu, so I stick with WebP and keep [caniuse.com/webp](https://caniuse.com/webp) bookmarked for skeptical stakeholders.

4. **Dial in WebP settings**  
   - Width: `1080px` (hard requirement for my handoffs)  
   - Height: leave blank so the aspect ratio stays honest  
   - Quality slider: `70%` A sweet spot between fidelity and weight for WordPress galleries  
   If you're exporting multiple formats, Affinity remembers per-format settings, so you can keep WebP lean without trashing PNG quality.

5. **Tweak macros (optional but recommended)**  
   There's a *Macros* dropdown in the same window. I run a tiny macro that scrapes EXIF + GPS metadata so no one leaks camera info. You can stack other edits too (like auto-levels), but I keep the batch pass focused on prepping assets.

6. **Run it**  
   Hit **OK**, watch the progress bar chew through the pile, and you're done. No manual babysitting, no plugin roulette.

## Notes after a few projects

- Affinity happily converts dozens of files at once, so I toss in all hero, blog, and thumb assets before zipping them into the repo.
- If a client insists on retina-sized imagery, I duplicate the batch job, swap width to 2160px, and slap `@2x` in the output naming pattern.
- This workflow is idiot-proof enough that I drop a short Loom for clients so they can refresh assets themselves when I'm off the clock.

Sure, there are other automation-friendly tools out there, but Affinity's batch job is the lowest-friction setup I've found that still respects quality controls. Free, fast, portable ticks every box when I'm wrapping a WordPress build.

Can you imagine, in 2025, now that these type of conversion is finally accesible? 

> - *Post Changelogs*
>   - *16th Dec 2025 - Publish Date*
