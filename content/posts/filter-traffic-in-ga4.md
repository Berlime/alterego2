---
title: "Filter Traffic in GA4"
description: "Do not track traffic from internal."
date: 2025-01-12
# image: ""
lastmod: 2025-01-13
showTableOfContents: false
tags: ["dev", "agency",]
type: "post"
---

I used WordPress the most, setting up Google Analytics is easy with WordPress, thanks to the Google Site Kit plug-ins,
or any other plug-ins that can easily integrate with Google Analytics.

One of the new goals in 2025 is to revamp my agency's main [website](https://berlime.com) with entirely new stacks. Meaning
it does not run on WordPress like before, just for that sake of exploring more options and learn new things. More on that in another post.

I recently look into how do I add Google Analytics in this blog, [hugo](/posts/hugo).
It quite straight forward thanks to this theme's [guide](https://gokarna-hugo.netlify.app/posts/theme-documentation-advanced/#analytics).

## Remove internal traffic

Sure, you want to track some traffic on your websites, but how do we not track traffic from our own devices.

I just did a simple Google search on "how to not track my own device in Google Analytics?"

Then, this article from Google appeared on the top. [Click here to see the Google's Guide](https://support.google.com/analytics/answer/10104470?hl=en).

Basically, here is what you can do, not only that you filter out your own visits:

- You can set to not track the whole network, in my case, it is my house. Filter out tracking from any traffic that comes from my house, which if the device is connected to my house Wi-Fi.
- You can even filter out traffic on an individual device level. It won't track if you use a device, regardless of what internet network you are connected to. In my case, I set it to not track from my mobile phone.
- I also set to not track my IPv6 addresses, just in case.

## This is entirely great for much more accurate analytics

My agency provides SEO services. These small things contributes to the value on what my agency can offer, not just blatantly slapping keywords and stuffs.
Believe me, there are a lot of agencies that just say what you want to here and literally did nothing at the back end. Because they would say "nah, you don't need this" :fire: :man_shrugging:

> - *Post Changelogs*
>   - *12th Jan 2025 - Publish Date*
