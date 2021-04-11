---
layout: post
title: "Introducing HODL Monitor"
date: 2021-03-21 00:00:00 -0500
author: Jason Lutterloh
excerpt_separator: <!--more-->
image: /assets/posts/post_crypto.png
excerpt: "Introduction to HODL Monitor - A Progressive Web App that will allow you to securely keep track of your crypto holdings' value without complicated sign-ins or APIs."
---

A month ago I published an open source app called Crypto Value Monitor (worst name ever). The app was super simple and was only geared at crypto hodlers who were also developers and knew how to run a web app locally. Unfortunately, I quickly realized even I didn't want to use this app if it wasn't available on my phone.

**So, I gutted the whole thing and re-built it.**

## Introducing HODL Monitor

My new description for the app is "A Progressive Web App that will allow you to securely keep track of your crypto holdings' value without complicated sign-ins or APIs."

Aside from the UI improvements (icons, slick transitions, color theme change), there's no longer a need to sign-up for your own API key and save that off in a file anywhere. I migrated from Nomics API (which was excellent but required a personalized API key) to CoinCap's API which doesn't require an API key. Also, CoinCap provides a websocket endpoint to get pricing which is pretty nifty. This allows for real-time price updates!

However, I'm most proud to be able to provide this app without any sort of privacy infringement. There's no sign-ups needed and no server-side tracking. That comes with a little bit of a cost (no backups, reliance on localstorage, etc) but I think that's a cost worth living with. I do intend to try and build a manual backup feature in the future though.

Anyways, take a look and try it out at [HODL Monitor](https://hodl.lutterloh.dev). If you're interested in the source code, that's available on GitHub at [HODL Monitor](https://github.com/jasonlutterloh/hodltracker).

UPDATE: I migrated to CoinGecko's API since they had a much more expansive set of cryptos. No websocket but that's okay.